---
layout: post
title: Factory reset of Cisco E20
date: 2010-10-11 15:59
author: tomlarse
comments: true
categories: [Cisco, E20, Tandberg, video conferencing]
---
To reset Cisco E20 to factory defaults, press:
´´´** -&gt; PC/Presentation -&gt; ##´´´
in less than three seconds

or

log in to the TSH CLI via telnet or SSH and enter the following:
´´´<code>xCommand systemunit Configuration ResetToFactoryDefaults Settings: All</code>´´´
