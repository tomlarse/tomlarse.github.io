---
layout: post
title: Cisco Meeting Server powershell module v0.4
date: 2016-09-30 19:01
author: tomlarse
comments: true
categories: [Uncategorized]
---
So the Acano server got released in version 2 almost two months ago, and with that changed name to Cisco Meeting Server as a result of the Cisco aquisition. The PsAcano powershell module of course needed a name change as well, so the module is now called PsCms.

All functions have had their prefix changed from Acano to Cms, so for instance Get-AcanoCall is now called Get-CmsCall and so on. I've added all the old function names as aliases for the new names, so existing scripts should not be broken.

I've also added all the changes that was made to the API in CMS 2.0 as well.

So without further ado, here's <a href="https://github.com/tomlarse/PsCms/releases/tag/v0.4" target="_blank">PsCms version 0.4</a>!
