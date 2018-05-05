---
layout: post
title: Presence issues with the calendar integration in CU2?
date: 2011-05-20 10:55
author: tomlarse
comments: true
categories: [bugs, errors, Lync 2010, Presence, Unified Communications]
---
I just had a case where the users experienced that presence in the Lync client did not update based on the calendar information unless they restarted the client completely. Relogging did not help.

The weird thing was that on the users contact card they would be listed as busy, but their presence was still available.

<img class="alignnone size-full wp-image-313" title="presence" src="http://codesalot.files.wordpress.com/2011/05/presence.jpg" alt="" width="306" height="318" />

After quite a bit of troubleshooting and some help from colleagues, I ended up removing CU2 (the April 2011 update, gives version .275 to the client). This removed the problem completely. So, if you are having presence issues with Lync, try removing CU2 for now.

This might be a bug?
