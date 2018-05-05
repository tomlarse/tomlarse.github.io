---
layout: post
title: Powerpoint presentations not working externally
date: 2013-09-27 11:15
author: tomlarse
comments: true
categories: [errors, external access, Lync, Lync 2013, Office Web Apps Server, Powerpoint, Reverse Proxy, TMG, Unified Communications, WAC]
---
I just had a problem with powerpoint presentations in Lync 2013 that behaved strangly.

All internal users could share and view powerpoints as they should, but all external users and guests could not. It behaved the same way in Lync 2013 clients as in the web app. It would just show "connecting" or "Waiting for the presentation to begin" before failing with a message that the network had gone down or the server was busy. There were no errors logged on the WAC server and no failures recorded on the monitoring database. I could also reach the https://wacserver.contoso.com/hosting/discovery through the TMG rule. Really weird.

After a bit of googling I found a <a href="http://social.technet.microsoft.com/Forums/lync/en-US/ef6136ad-3115-44ef-8574-cdba76e2233d/remote-users-unable-to-view-power-point-presentations-on-lync-2013">forum post</a> on technet where someone referenced a setting on the HTTP filter called "Verify Normalization". The setting is found on the "Traffic" tab on the rule, like this:

 <img src="http://codesalot.files.wordpress.com/2013/09/capture.png" alt="Verify Normalization" width="512" height="614" class="alignleft size-full wp-image-516" />

Unticking this box solved the issue.

The rule is explained <a href="http://blogs.technet.com/b/isablog/archive/2006/05/02/427002.aspx">here</a>, but it is basically a security mechanism that blocks URLs containing % sign if they are double encoded in the URL, although they can end up blocking legitimate traffic as well which is the case here. I do not know if this is a bug in WAC/OWAS or if it is by design though. Removing "Verify Normalization" from the rule will solve the issue in any case. 

The URL the clients were accessing looked something like this, and contains a lot of url encoded characters.

https://lync-app.domain.no/m/Presenter.aspx?a=0&amp;e=true&amp;WopiSrc=https%3A%2F%2Flync-fe1.domain.no%2FDataCollabWeb%2Fwopi%2Ffiles%2F9-1-2C3E7AD&amp;access_token=AAMFEOV5-KFUGNRfrclZBRMAVS8GEC3yB9HdElYrtUpQ8UkEs2KBEOV5-KFUGNRfrclZBRMAVS-CAr65gyAPlwe3U3NwCIa-PNE_Q7U3BPbx_s-yipQjZy9FKfOs04YIc2BBOb2J0AgIDURhdGFDb2xsYWJXZWI&amp;&lt;fs=FULLSCREEN&amp;&gt;&lt;rec=RECORDING&amp;&gt;&lt;thm=THEME_ID&amp;&gt;&lt;ui=UI_LLCC&amp;&gt;&lt;rs=DC_LLCC&amp;&amp;gt 
