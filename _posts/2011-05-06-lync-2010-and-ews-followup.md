---
layout: post
title: Lync 2010 and EWS followup
date: 2011-05-06 16:04
author: tomlarse
comments: true
categories: [Uncategorized]
---
This is a followup to <a href="http://www.codesalot.com/2011/lync-2010-and-exchange-web-servicesautoconfigure/">this</a> post.

Turns out that Outlook doesn't really like autodiscover through SRV records and proceeds to ask the user for authentication when this happens. This is often not a desireable situation.

The other option seemed to be to add names for autodiscover.domain.com for each of the SMTP domains to the certificate on the CAS. We tried this as well, but in this configuration the Lync client started asking about trust of the server. A bit of searching led me to <a href="http://blogs.technet.com/b/jenstr/archive/2011/02/10/lync-cannot-verify-that-the-server-is-trusted-for-your-sign-in-address.aspx">this</a> post by Jens Trier Rasmussen that explains why.

I was not able to find any place to add trusted servers to Lyncs trusted server list, but for Outlook i could, so the solution was to revert to SRV records, and add this regkey to the machines:

[code]

Office 2007:
HKCUSoftwareMicrosoftOffice12.0OutlookAutoDiscoverRedirectServers

Office 2010:
HKCUSoftwareMicrosoftOffice14.0OutlookAutoDiscoverRedirectServers

[/code]


add the CAS server FQDN as the value name of a key with value type REG_SZ and empty value data.

This tells Outlook to always trust this server.
