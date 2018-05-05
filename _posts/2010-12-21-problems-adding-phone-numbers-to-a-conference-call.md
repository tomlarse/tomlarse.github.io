---
layout: post
title: Problems adding phone numbers to a conference call
date: 2010-12-21 12:10
author: tomlarse
comments: true
categories: [enterprise voice, OCS 2007 R2, Unified Communications]
---
I've recently had some problems with an OCS 2007 R2 installation where the users were complaining that they couldn't add external phone numbers to a conference call. Internal numbers and SIP contacts were working fine.

I did some tracing, and noticed that the service provider gateway returned a 404 Not found when answering to the SIP Invite of the phone number. I checked the number, and it seemed correct.

But the FROM: field of the INVITE was populated with the users SIP URI not the users TEL URI, which the service provider didn't handle. Normally a call through the mediation server will use the TEL URI, but turns out that it doesn't in this case. There is AFAIK no way to handle this in OCS 2007 R2. (There might be in Lync, but I'll need to lab that. The conference call behaves the same way in Lync, but you have the option to substitute the dialed from number on the route.)

This means that the service provider needs to handle this and substitute all unknown URI's in the FROM: field with some known number, ex. the Dial In conference number or the main number of the organization, unless the service provider wants to maintain a database of the users and their corresponding TEL URI.

It might also be a solution to put some kind of gateway between the PSTN and OCS that does the conversion.

Has anyone else seen this?
