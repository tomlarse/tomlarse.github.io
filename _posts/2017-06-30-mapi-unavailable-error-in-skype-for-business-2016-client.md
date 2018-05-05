---
layout: post
title: "MAPI unavailable" error in Skype for Business 2016 client
date: 2017-06-30 07:18
author: tomlarse
comments: true
categories: [Uncategorized]
---
There are some situations described in this kb, https://support.microsoft.com/en-us/help/3147130/mapi-unavailable-error-in-skype-for-business-2016-client, that will generate a popup in the client saying "Your Outlook profile is not configured correctly" and MAPI status under configuration information will show ""MAPI Unavailable"

In the KB Microsoft describes a workaround, but it involves quite a lot of steps, so I made a small Powershell script that will do the job for you. The script needs to run in the context of the user with the problem, as it uses outlook to get the LegacyDN attribute.

[gist]b13b08f193ece95b02db7ea133573241[/gist]
