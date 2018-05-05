---
layout: post
title: Manage Acano server with Powershell: PSAcano version 0.3 released
date: 2016-06-07 17:51
author: tomlarse
comments: true
categories: [Uncategorized]
---
Acano server 1.9 was released 6.6.2016, and with it came some new features, most notably the ability to record meetings within the Acano server.

This also means that the API has been updated, so PsAcano needed an update as well. PsAcano version 0.3 adds all the new parameters and the entire new recording possibility to the module.

The release can be downloaded from <a href="https://github.com/tomlarse/PsAcano/releases/latest" target="_blank">here </a>or you can run

[sourcecode language="powershell"]iex (New-Object Net.WebClient).DownloadString(&quot;https://gist.githubusercontent.com/tomlarse/5f43bbe0e763cea379ca/raw/83054527ca5e5433e466f55106ea145bec330435/installmodule&quot;)[/sourcecode]

in powershell to install the module.

As always, please report <a href="https://github.com/tomlarse/PsAcano/issues" target="_blank">issues</a>, and feel free to contribute if you feel you have anything to add!

&nbsp;

&nbsp;
