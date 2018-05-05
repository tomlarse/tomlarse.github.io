---
layout: post
title: URI dialing domain check
date: 2011-01-25 11:45
author: tomlarse
comments: true
categories: [DNS, URI Dialing, video conferencing]
---
I made a quick and dirty php script to check if your domain is correctly configured in DNS to support standards based URI dialling. Just input your URI domain and your target gateway, and the script will check if the SRV records are correctly configured and that the A record for the gateway exists.

I'll add more functionality and nicer looks as time goes by :P feature requests in comments.

<a href="http://www.codesalot.com/dnscheck/">http://www.codesalot.com/dnscheck/</a>
