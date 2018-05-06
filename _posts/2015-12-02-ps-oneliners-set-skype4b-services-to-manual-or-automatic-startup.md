---
layout: post
title: PS Oneliners: Set Skype4B services to manual or automatic startup
date: 2015-12-02 09:22
author: tomlarse
comments: true
categories: [Oneliners, powershell, script, Scripts, Skype for Business, Unified Communications]
---
If you need to reboot a Skype for Business server, you might not always want the services to start automatically afterwords for various reasons. For instance if you are doing a shutdown of an entire pool, you'd want to run
<pre>Start-CsPool -PoolFqdn skypepool.contoso.com</pre>
to do a cold start of the pool, instead of the services starting automatically.

Use these oneliners to set the services to manual startup and back again to automatic afterwords.

{ % gist 2b516ddcbde1341541de % }
