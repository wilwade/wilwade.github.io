---
layout: post
title: "When the Cloud API Changes"
description: ""
category: Projects
tags: [BrowseTheRiver.com, api, cloud]
---
{% include JB/setup %}

### Update: 2014:
Browse the River was shut down at the end of 2014.

---

www.BrowseTheRiver.com has been up and running for a little while when I received an unwelcome email.

Amazon periodically edits their Product Advertising API. Generally it is to add features, combine them in different ways, and to remove features that are either costing them too much money or that no one is really using.

This time around they modified a feature that limits the maximum number of results you can receive from a single query. Currently the limit is 400 pages of results each containing 10 results. The new limit will be 10 pages still with 10 results per page. Now Amazon likely thought why on earth would someone really want 4,000 results from a single query? Would not 100 be enough?

Browse the River is likely the only legitimate service using the other results. Because Browse the River does not always want common results, we use random results from anywhere in the range of 1-4,000 sorted by best selling. The idea behind Browse the River is that those oddball results were fun and interesting.

I am not sure how common this is for small sites like Browse the River that are developing, but it is not necessarily bad. In the following few weeks we will be reevaluating our focus and seeing what new purpose we can give Browse the River. We will let you know how it goes.

Until then keep checking out what random items you can find on www.BrowseTheRiver.com. 