---
layout: post
title: Tandberg TCAP Day 3
date: 2008-08-08 07:06
author: tomlarse
comments: true
categories: [Codian MCU, Tandberg, TCAP, video conferencing]
---
Todays topic is The Tandberg Codian MCU 4500 series<br /><br />I do not know anything about the codian at all, so today will be purely lecture notes. The references to pages are pages in the course material.<br /><br />The main difference between the 4500 series and the 4200 series is the amount of DSP chips. Also the 4200 has no support for Tandberg Codian ClearVision and if you want to have a higher resolution than CIF, you need to order an upgrade option.<br /><br />ClearVision is described on page 16, but allows video media to be enhanced by up to 4 times the original resolution.<br /><br />The 4200 uses an additional port for streaming. The 4500 does not. See amount of ports on page 22.<br /><br /><br />The codian MCU has two types of prefixes, a service prefix which is the same as on the MPS, but it also has a prefix that will register the full number on the gatekeeper. This can be used if you have a border controller and are allowing calls from the outside, by denying outside callers to call your internal conferences that are using your service prefix, but allow calls to external conferences which uses the GK registration prefix.<br /><br />All conferences need to have a unique name, and it cannot be the same as old conferences either. It is therefore important to purge old conferences from time to time.<br /><br />On versions 2.0 and older, you have to do a factory reset to recover a lost password, see page 88. On version 2.1 and newer, there is a reset password command on the console interface, see page 86.<br /><br />And I passed the test :D I am now Tandberg TCAP!
