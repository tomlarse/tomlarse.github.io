---
layout: post
title: Address book issues
date: 2010-10-11 15:54
author: tomlarse
comments: true
categories: [Address book service, Certificates, OCS 2007 R2, Unified Communications]
---
I had a weird problem with an 2007R2 installation last week. The addressbook had stopped working. I checked all the normal errors, certificates and IIS on the FE, but everything seemed to be just fine. The addressbook files were created, and I could download all files in the browser. Everything seemed to be normal, except that the clients were giving the error about not being able to download the addressbook.

After a bit of searching the internets, I came across <a href="http://www.theocsinsider.com/ocs-2007/ocs-and-windows-7-problems-to-watch-out-for/" target="_blank">this</a>. Seems that there was some new functionality added to IE8 where it refuses the certificate if the CRL is unreachable.

The solution is either to fix the CRL, or to uncheck "Check for server certificate revocation" under advanced settings in &gt;IE8.
