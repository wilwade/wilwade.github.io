---
layout: post
title: "Random Rows from a Database Cache Table"
description: ""
category: code
tags: [MySQL database query]
---
{% include JB/setup %}

Here is a slight problem I had the other day.  I had a need to retrieve a single random row from a database table that was caching some items with several conditions:

 - The rows in the database were constantly changing
 - There could be a very large number of rows (20,000)
 - There could be a small number of rows (2)
 - A count of rows in the table could become incorrect within milliseconds
 - Must be fast


I know this is likely a uncommon set of conditions.  It would appear to be from the large number of posts regarding random rows from databases.  Most of the solutions have items in direct contrast with some of my conditions.  For example most databases have some form of this MySQL code (see a [nice list from Pete Freitag](http://www.petefreitag.com/item/466.cfm))

{% highlight SQL %}
SELECT column FROM table
ORDER BY RAND()
LIMIT 1;
{% endhighlight %}

However for large datasets is very slow ([See the multitude of complaining about it](http://www.google.com/search?q=mysql+rand+slow)). Thus as it violates a set of conditions it is useless.

There are many [posts about using the number of rows or the a table](http://akinas.com/pages/en/blog/mysql_random_row/) without holes in an auto increment field, but these were also unhelpful.

A few do a double call to the database, one to get the number of rows and then another with a limit like so:

{% highlight SQL %}
SELECT column FROM table
ORDER BY RAND()
LIMIT "[random from table count]","[number of rows]";
{% endhighlight %}

This would almost work until I remembered this fact about my project: After I used a row once, it would be deleted or anything older than an hour would also be deleted.  All the table really is a cache where we throw already mostly random items.  And depending on the number of users that means that my table row count could be changing quickly.

So the solution I came up with for a random cache table row is on the insert side of things.

Add a column to the table say randomColumn. Likely you will want to index the column for faster ordering on the other end.

Generate a random number between 1 and say 100.  Increase your upper limit for greater randomness. You can also have \[my\]SQL generate the number for you, but likely it is faster for PHP or whatever you are coding in. ```FLOOR(8 * RAND()) + 1``` will give you a random number in MySQL.

{% highlight SQL %}
INSERT INTO table
(data, randomColumn) VALUES (Some data, "[Generated Random Number]"");
{% endhighlight %}


Then on the select side order by the randomColumn.

{% highlight SQL %}
SELECT * FROM table
ORDER BY randomColumn
LIMIT "[number of rows]";
{% endhighlight %}

Now you are inserting your columns into a "random order" and the speed loss of generating a random number for each row with each column is gone!  Also since the columns are being deleted after use this will always bring up a new "random" row.