---
layout: post
title: Making Office Web Apps Server private
date: 2013-10-03 21:28
author: tomlarse
comments: true
categories: [Lync 2013, Office Web Apps Server, powershell, Reverse Proxy, security, Unified Communications, WAC]
---
After installing the WAC server following <a href="http://ucdaily.net/2013/01/16/installing-the-office-web-apps-server-for-lync-server-2013/" title="this" target="_blank">this</a> or another guide, we also normally publish the WAC server through the same reverse proxy method as we do the other Lync web services - using the DNS name that we configured when we created the farm. 

If you publish the WAC server this way without doing anything else it will work the same way for users on the internet as it does for the internal users and we might be content with that. But should we? 

My colleague Marjus made <a href="http://marjuss.wordpress.com/2013/05/03/basic-security-better-than-no-security-limit-access-to-office-web-apps-server/" title="post" target="_blank">this</a> post a little while back on how to limit the access to the WAC services only to servers from your domain. If you don't do this you're basically publishing the WAC server as a public service that anyone can add to topology builder and use as the WAC server in their own Lync environment. 

So, if you want to keep your WAC server for yourself, remember to add all domains where you host servers that should be able to use the WAC server to the allow list by using the <a href="http://technet.microsoft.com/en-us/library/jj219459.aspx" title="New-OfficeWebAppsHost" target="_blank">New-OfficeWebAppsHost</a> Cmdlet. The wildcard * is assumed on all domains in the allow list, so subdomains are supported automatically. You only need to add the server domain(s), not necessarily the same as the SIP domain(s). 

```
New-OfficeWebAppsHost -Domain &quot;contoso.com&quot;
```
