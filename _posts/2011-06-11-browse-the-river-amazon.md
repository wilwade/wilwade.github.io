---
layout: post
title: "Browse the River Amazon"
description: ""
category: Code
tags: [BrowseTheRiver.com, sql]
---
{% include JB/setup %}

### Update: 2014:
Browse the River was shut down at the end of 2014.

---

For normal people:
I have a little web startup: www.browsetheriver.com.  You should go check it out!

For programmers:
Of the greatest things that the web has spawned is the extension beyond the simple links of the 90's to the APIs of today.  Google, Twitter, and Amazon all have amazing things that you can go with their services without much hacking.

For browsetheriver.com it took a bit of hacking on the Amazon Product API for it to work correctly.

Basically BtR does nothing more than pull a random product out of the tens of thousands of products that Amazon offers in one way or another.  Easy sounding, but not so easy to have actually happen.  Amazon does not allow just any search and on each search you can only get to the first 400 results, and you only get 10 results per actual request, and only 2000 requests may be made per hour.

So I ended up doing this method:

Each time we want a random product we actually pull the top one from a database table sorted by a random number that was generated at entry.  (This works because once the information on the product is retrieved, that item in the database is deleted.  For more information see my post: "Random Rows from a Database Cache Table")

That product information is placed in the field for the retrieval by javascript to load that when someone requests it.  When that information is in use, there is an ajax request in the background both for the next item (from the database cache) and to a page that adds 10 new results from Amazon into the cache.  (It also deletes anything over an hour old in the cache.)

In this way you quickly get the next random product from Amazon and I get 20,000 random products per hour.

Check out the result at www.browsetheriver.com and let me know if you find any bugs!