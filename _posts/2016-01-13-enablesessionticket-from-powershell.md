---
layout: post
title: EnableSessionTicket from Powershell
date: 2016-01-13 12:38
author: tomlarse
comments: true
categories: [Lync, Oneliners, powershell, Scripts, Skype for Business, Unified Communications]
---
To get support for Lync and Skype for Business on Windows Server 2012 R2, you need to add a registry key that changes TLS session caching on 2012 R2 Server. This is described here https://support.microsoft.com/en-us/kb/2901554

To create this key, use the following powershell oneliner:

{% gist 3172ef0e5a981da53534 %}
