---
layout: post
title: Error code 1603 - Skype for Business upgrade
date: 2015-05-04 13:42
author: tomlarse
comments: true
categories: [errors, Skype for Business server 2015, skype4B, Uncategorized]
---
Skype for Business server 2015 is here, and with it comes a time for "firsts". Today, I've done my first In-place upgrades on servers from Lync 2013 to SfB 2015.

One thing I noted on a couple of servers was that the install failed during "Installing local management services" with this error:
<pre style="margin:0;font-family:Calibri;font-size:11pt;"><span style="color:#ff0000;">Error returned while installing OcsCore.msi(Feature_LocalMgmtStore), code 1603.
</span>´´´
I tried the "retry" option in the wizard, but it did no difference. A reboot of the server did the trick in both instances and the install continued perfectly.

I saved the logs and went through them afterwards, and found these lines
´´´Error 0x80070430: failed to set security info for object: RTCCLSAGT error code: 1072
Error 0x80070430: failed to set security info for object: REPLICA error code: 1072´´´
A quick google search shows that this error means "The specified service has been marked for deletion." So for some reason the wizard hasn't been able to completely delete the service. Seems that the easiest way to resolve this error is a quick reboot of the server, but to avoid getting it here's a couple of checks:
<ul>
	<li>Be sure to have closed all mmc instances on the server, including
<ul>
	<li>Services</li>
	<li>Event viewer</li>
</ul>
</li>
	<li>Close Task manager</li>
</ul>
I'm pretty sure there are other causes for the error as well, but again, in all cases a reboot should solve the issue.
