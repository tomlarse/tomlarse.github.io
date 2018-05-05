---
layout: post
title: Lync 2010 and Exchange Web Services/autoconfigure
date: 2011-03-03 13:43
author: tomlarse
comments: true
categories: [Autoconfigure, Calendar Sync, EWS, Exchange, Lync 2010, Presence, Unified Communications]
---
I've recently been upgrading an OCS 2007 R2 environment to Lync 2010 where the users have SMTP adresses in several SMTP domains, but they only have one SIP domain. All users have an SMTP address at least in the SIP domain, but many of them have their primary SMTP address in different domains from the SIP domain.

What happened when we migrated the first couple of users to the new Lync FE pool and the new client, some of them lost their calendar integration and recent calls list. It was early apparent that these users were the ones that didn't have their primary SMTP address in the SIP domain, so at least we were able to find a common denominator.

Taking up the configuration information on the client showed "EWS not deployed" and the fields for EWS Internal and External URL were empty. Testing autoconfigure in Outlook did not return any errors. Of course google is my friend, so I found <a href="http://www.confusedamused.com/notebook/lync-claims-ews-not-deployed/" target="_blank">this</a> post at confusedamused that listed a couple of things to check. None of these solved it for me, but check them first in any case.

When more googling didn't result in any more possible solutions, I started looking at wireshark traces, and noticed that the Lync client was actually looking up DNS autoconfigure for the users primary SIP domain, not the SMTP domain. As it turned out, autoconfigure was set up to use SCP in all the other domains than the SMTP domain that was equal to the SIP domain, so the Lync client failed to get autoconfigure config for the other domains. I dont know why this was not a problem in R2, so theres probably been some kind of change to how the Lync client handles EWS configuration. Adding the autoconfigure host to HOSTS on the client machine I saw that the Lync client was getting "401 Unauthorized" messages back from the EWS server. I didn't notice at first, but it was trying HTTP, not HTTPS which had failed a couple of packets earlier, because EWS didn't have a SAN name in the correct domains.

The solution then was to either add autoconfigure names for the other domains to SAN on the EWS IIS certificate, or adding a SRV record pointing to the Exchange CAS for autoconfigure in the other domains. Hey presto!
