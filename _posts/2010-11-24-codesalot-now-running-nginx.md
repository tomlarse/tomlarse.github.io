---
layout: post
title: Codesalot now running nginx
date: 2010-11-24 12:13
author: tomlarse
comments: true
categories: [apache2, codesalot.com, General, nginx]
---
So I've had a lot of issues with the server running this site lately, basically related to apache2 hogging all system resources. I don't really know what happened, but apache suddenly started using a lot of swap (all of it), and system load average was around 16.

I've tried fixing it for a while, but now I gave up. The site is now running nginx and load average seems to have dropped to around 0.03 now :D

Thanks to <a href="http://matthewhelmke.net/2009/01/08/a-short-howto-apache-to-nginx/">http://matthewhelmke.net/2009/01/08/a-short-howto-apache-to-nginx/</a> for the howto migrate!
