---
layout: post
title: What to do if users are enabled for LCS?
date: 2011-04-06 15:06
author: tomlarse
comments: true
categories: [LCS 2005, Lync, Migration, Unified Communications]
---
I just had a Lync installation where it turned out that about 5 years ago they had tried installing LCS 2005 in AD, an installation that had failed and the servers had been taken down without being disabled.

The users that had been enabled that time was therefore still enabled for LCS in AD, and first of all did not appear when trying to search for them in the "enable users" UI. Searching for them with "Legacy users" filter on showed them, but failed when trying to move them with the "Move users" script in BigFin. It is also not supported to move LCS enabled users to Lync. Disabling them in BigFin will also not work. The error message will say something about users not enabled for rich presence, which was added in 2007 R2.

What will work though is the cmdlet Disable-CsUser. Run the cmdlet on the affected users, and then enable them as a normal non-enabled user again after that. I guess that old buddy lists and settings from LCS will be removed by this as well, so it is not a recommended migration path though. In my case this was not important.
