title: Handling SimpleURLs and Reverse Proxy during migration
link: http://blog.codesalot.com/2013/06/13/handling-simpleurls-and-reverse-proxy-during-migration/
author: tomlarse
description: 
post_id: 495
created: 2013/06/13 10:39:37
created_gmt: 2013/06/13 10:39:37
comment_status: open
post_name: handling-simpleurls-and-reverse-proxy-during-migration
status: publish
post_type: post

# Handling SimpleURLs and Reverse Proxy during migration

I've thought about writing this post for a while, as the topic isn't really covered very well in the Lync 2013 [migration documentation](http://technet.microsoft.com/en-us/library/jj205369.aspx). The issue is also only relevant when migrating from Lync 2010 to Lync 2013.

## Comments

**[Ahmed Fouad](#358 "2013-10-26 16:21:09"):** Thanks for the article. But you will still need to use a different Simple URLs.

**[Tom-Inge Larsen](#359 "2013-10-28 09:51:19"):** Hi

**[practicallync](#398 "2013-11-24 14:17:43"):** Thank you!! Wish I found this earlier. :-)

**[pete](#435 "2014-02-11 20:02:58"):** We are seeing these symptoms but for both internal and external users. 2013 users even while within the office cannot get to the meet url with the errors you mentioned above.

**[Trey Gross](#392 "2013-11-14 22:55:48"):** ok I did that on my TMG but if I have the 2010 reverse proxy as rule 1 than all works for 2010 pool members, rule 2 is on there for 2013 it seems to work and takes a long time to finally error out.

**[Tom-Inge Larsen](#393 "2013-11-14 23:01:36"):** This might be a million things. does the rule work if you test it? is the external services on the fe working?

**[henrikborjesson](#2602 "2014-11-05 09:19:20"):** Reblogged this on [Henrik Börjesson's UC-Blog](http://henrikborjesson.wordpress.com/2014/11/05/handling-simpleurls-and-reverse-proxy-during-migration/) and commented:

**[henrikborjesson](#2603 "2014-11-05 09:20:46"):** Thx Tom-Inge

