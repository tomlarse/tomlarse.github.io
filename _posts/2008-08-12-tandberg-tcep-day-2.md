---
layout: post
title: Tandberg TCEP Day 2
date: 2008-08-12 07:08
author: tomlarse
comments: true
categories: [Border Controller, Gatekeeper, Tandberg, TCEP, VCS, video conferencing]
---
Todays topic is Bandwith and call control

There will also be a test today.

To be able to call out on the internet on the VCS, you need to add the DNS Zone. It should only be added on the Express, not on the control. It will not be there by default. On the Gatekeeper/BorderController this is not necessary.

If you are neighboring gatekeepers, you need to use a pattern type to reach the endpoints on another gatekeeper. It will work fine without, but if you plan to use bandwith control the call will not be in the correct link if you don't use a pattern. This is possibly a bug, and will probably be fixed in version X3.

SIP &lt;-&gt; H.323 interworking will also work when contacting an endpoint on the outside, but it will consume 1 ekstra traversal license because of the interworking, so it will use 2 traversal licenses.

And I passed the TCEP as well :)
