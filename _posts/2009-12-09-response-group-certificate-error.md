---
layout: post
title: Response group certificate error
date: 2009-12-09 14:02
author: tomlarse
comments: true
categories: [OCS 2007 R2, Response Group Service, Unified Communications]
---
Got a certificate error when i tried starting the response group service today.

<em>The provided certificate is not valid. </em>

<em>There was a problem validating certificate: Identity check failed for outgoing message. The expected DNS identity of the remote endpoint was '&lt;poolname fqdn&gt;' but the remote endpoint provided DNS claim '&lt;fqdn in a sip domain&gt;'. If this is a legitimate remote endpoint, you can fix the problem by explicitly specifying DNS identity '&lt;fqdn in a sip domain&gt;' as the Identity property of EndpointAddress when creating channel proxy.</em>

Turns out that the last SAN in the certificate needs to be the same as the CN in the certificate, which should be your pool FQDN. The service will fail if it isnt.
