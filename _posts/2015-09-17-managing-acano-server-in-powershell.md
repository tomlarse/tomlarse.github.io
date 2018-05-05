---
layout: post
title: Managing Acano Server in Powershell
date: 2015-09-17 20:37
author: tomlarse
comments: true
categories: [Acano, Lync, powershell, Skype for Business, Unified Communications, video conferencing]
---
v0.2 has been released! Post <a href="http://blog.codesalot.com/2015/12/04/manage-acano-server-with-powershell-psacano-version-0-2-released/" target="_blank">here</a>

I love it when stuff is possible to manage through PowerShell.

I've been working quite a bit with Acano lately and because of that I have started looking in to the management API that they provide on their Server. This API is exposed as XML through HTTPS, so I thought that it should be quite possible to write some PowerShell functions that accessed parts of the API. These have evolved in to what I now release as version 0.1 of the PsAcano PowerShell implementation of the Acano API.

Currently only the GET commands are implemented, so it is only possible to view information at the moment - not edit or create anything. The functionality provided by the POST, PUT and DELETE commands will  be implemented in the coming days and weeks.

Last weekend Knowledge Factory had our kick off in beautiful Vaxholm outside of Stockholm. There we were treated to an extremely inspiring session by <a href="https://twitter.com/simonwahlin" target="_blank">Simon Wåhlin</a> (http://blog.simonw.se/) about PowerShell and GIT. A big thank you to Simon for finally kicking me into doing source control on my scripts :D

I've set up an account on <a href="http://github.com/tomlarse" target="_blank">Github</a>, and from now on my scripts will be available there, and this of course also applies to <a href="https://github.com/tomlarse/PsAcano" target="_blank">PsAcano</a>.

If you don't want to visit the repository page on github, you can download the module <a href="https://github.com/tomlarse/PsAcano/releases/latest" target="_blank">here</a>. Installation instructions can be found in the Readme.md file. Feedback is welcome as issues on github or comments on this blogpost.
