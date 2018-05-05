---
layout: post
title: #Lync mobile hanging on "getting contacts"
date: 2012-02-07 10:50
author: tomlarse
comments: true
categories: [bugs, Lync, Mobility, Unified Communications]
---
I have just been troubleshooting a weird issue where a user complained about Lync mobile taking a long time signing in, and then  not showing the buddy list until several days after sign in. Push would also not work until after the contact list was downloaded.

After reading a lot of logs and traces and not finding anything we tried finding things that were different from this user and everyone else. It turned out he had added some Cisco video conferencing endpoints to his contact list. In a desperate attempt we tried deleting these from his buddy list, and the problem disappeared.

Seems that the mobile client has some issues getting presence from integrated SIP domains or something like that. I tried replicating the problem with my user, and managed to do so:

I added the Cisco E20 on my desk to my buddy list:

<a href="http://codesalot.files.wordpress.com/2012/02/capture.jpg"><img class="alignnone size-full wp-image-380" title="Capture" src="http://codesalot.files.wordpress.com/2012/02/capture.jpg" alt="" width="323" height="126" /></a>

And tried logging in on my iPad:

<a href="http://codesalot.files.wordpress.com/2012/02/photo-09-32-30-07-02-12.png"><img class="alignnone  wp-image-381" title="Photo 09 32 30 07.02.12" src="http://codesalot.files.wordpress.com/2012/02/photo-09-32-30-07-02-12.png" alt="" width="400" height="600" /></a>

The client is in norwegian, but it says "No contacts", and I guess "getting contacts" on the bottom.

This is what I see until I either delete the contact from my buddy list or wait for up to several days. In this state I can recieve IMs if I am in the client, but push does not work.

On my windows phone, the contact list is just empty, there are no messages of any kind and it has the same behavior, can recieve IMs, but no push.

I have not tried on an android yet.

I've tried reading through logs as well, but I can't figure out what is causing this, so the fix for now seems to be to delete those types of contacts
