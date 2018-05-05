---
layout: post
title: Office Communications Server 2007 R2 running on Windows Server 2008 service problems
date: 2009-03-10 10:11
author: tomlarse
comments: true
categories: [OCS 2007 R2, problems, services, Uncategorized]
---
I have on a couple of occations now experienced problems with the services on OCS 2007 R2, when running on 2008 server. I seems that the services hang during boot, and this causes all other services to halt startup as well.<br /><br />The first time i experienced this, the server seemed to hang on "Configuring updates" during boot, though this was not the case.<br /><br />The solution has been to either set all OCS services to "Automatic (delayed startup)", or to keep the front end service to "Automatic" and all other OCS services to delayed.<br /><br />I dont know why this happens, and I haven't been able to figure it out. If someone has an idea of why, please let me know.
