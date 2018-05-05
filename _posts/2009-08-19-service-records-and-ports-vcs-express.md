---
layout: post
title: Service records and ports, VCS Express
date: 2009-08-19 13:26
author: tomlarse
comments: true
categories: [DNS, Network, ports, Tandberg, VCS, VCS Express, video conferencing]
---
Here are the service records needed to use the Tandberg VCS:

_h323ls._udp.company.com      srv     1 0 1719 vcs-e.company.com.
_h323cs._tcp.company.com      srv     1 0 1720 vcs-e.company.com.
_sip._udp.company.com              srv     0 0 5060 vcs-e.company.com.
_sip._tcp.company.com               srv     0 0 5060 vcs-e.company.com.
_sip._tls.company.com                 srv     0 0 5061 vcs-e.company.com.
_sips._tls.company.com               srv     0 0 5061 vcs-e.company.com.
_sips._tcp.company.com             srv     0 0 5061 vcs-e.company.com.

There should also be an a-record pointing to the vcs express. (in this example, vcs-e.company.com)

Also, should anyone ever need it, here are the ports that an endpoint needs opened outbound if it is registering directly to a VCS express:

TCP/2776 (Q931/H245 for external traversal endpoints)
UDP/2776 (RTP Media from external traversal endpoints)
UDP/2777 (RTCP Media control traffic from external traversal endpoints)
UDP/1719 (H323 RAS signaling from gatekeepers/VCSes and traversal endpoints)
TCP/1720 (Q931/H.225 call connect signaling)

UDP/5060 (SIP signaling)
TCP/5060 (SIP signaling)
TLS/5061 (Encrypted SIP signaling)
