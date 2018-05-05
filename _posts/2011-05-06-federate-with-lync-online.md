---
layout: post
title: Federate with Lync Online
date: 2011-05-06 14:59
author: tomlarse
comments: true
categories: [Lync 2010, Lync Online, Office 365, Oneliners, Unified Communications]
---
To federate with Lync Online/Office 365, run:

[sourcecode language="powershell"]
 New-CSHostingProvider –identity LyncOnline –ProxyFqdn sipfed.online.lync.com –Enabled $True

Enable-CSTopology
 [/sourcecode]


Here's how to do it using GUI: <a href="http://techietom.co.uk/blog/2011/04/how-to-enable-office365-lync-online-to-federate-with-lync-on-prem/">http://techietom.co.uk/blog/2011/04/how-to-enable-office365-lync-online-to-federate-with-lync-on-prem/</a>
