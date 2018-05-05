---
layout: post
title: Audio delay when answering call
date: 2010-04-21 21:35
author: tomlarse
comments: true
categories: [Mediation Server, OCS 2007 R2, Unified Communications, Windows Firewall, Windows Server 2008]
---
I've been having some trouble lately with call setup on incoming calls. After the call has been answered, there has in some cases gone up to 8-9 seconds before you can hear the person on the other side. Obviously this is quite a pain...

When trying to google the problem you get a lot of posts telling you to disable Windows Firewall. This actually solves the problem so if you are content with just disabling a firewall without knowing why, you can stop reading now.

Seems that when you install the mediation server on a Windows Server 2008 the firewall fails to open the proper UDP port negotiated during the RFC 3690 Early media negotiation until Windows Firewall detects an outgoing UDP stream. This can be solved/worked around by adding an inbound rule in the firewall that allows all UDP ports.

Thanks to <a href="http://blogs.technet.com/jeffnye/archive/2009/06/17/early-media-and-windows-server-2008-firewall.aspx">JeffNye</a> for tipping me in the right direction!
