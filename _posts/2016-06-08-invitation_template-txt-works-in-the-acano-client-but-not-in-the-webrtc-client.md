---
layout: post
title: Invitation_template.txt works in the Acano Client, but not in the WebRTC client
date: 2016-06-08 16:34
author: tomlarse
comments: true
categories: [Uncategorized]
---
I've been delivering an Acano Certified Engineer II class this week, and one of the labs is to create call branding for the Acano lab deployment.

On the Acano server you can customize the meeting invitation by using a template file uploaded to a webserver. What happened in the lab was that all the students were able to see the custom template work in their Acano clients, but when they logged in to the webRTC client on the webbridge, it fell back to the default template.

We found a file from a known working deployment and used that, and suddenly it started working in both clients. So at least we knew that the file itself was the problem. A couple of the students compared the files, and the working one was encoded as UTF-8 while the non-working one was encoded as UTF-8-BOM. The Acano docs states that the file needs to be UTF-8 encoded which they are, and apparently the Acano client handled the BOM addition fine while the webbridge didn't.

After googling a bit it seems that windows notepad is not capable of saving UTF-8 without BOM, so the solution ended up being to use notepad++ and save it as UTF-8 without BOM there.
