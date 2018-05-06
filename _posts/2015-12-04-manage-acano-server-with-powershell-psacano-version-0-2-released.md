---
layout: post
title: Manage Acano server with Powershell: PSAcano version 0.2 released
date: 2015-12-04 11:48
author: tomlarse
comments: true
categories: [Scripts, Unified Communications, video conferencing]
---
v0.1 post is <a href="http://blog.codesalot.com/2015/09/17/managing-acano-server-in-powershell/" target="_blank">here</a>

I've finally gotten time to complete coding of the 0.2 release of the PSAcano powershell module.

The module now contains all GET, POST, PUT and DELETE commands from the <a href="https://www.acano.com/publications/2015/09/Solution-API-Reference-R1_8.pdf" target="_blank">Acano API documentation</a>, and everything that is possible to do with the API should now be possible to script in powershell.

Error handling is still not in the module, this is planned for the 0.3 release, I'll be adding that the next couple of weeks.

You can download the latest release <a href="https://github.com/tomlarse/PsAcano/releases/latest" target="_blank">here</a>, or you can clone the project with Git from <a href="https://github.com/tomlarse/PsAcano" target="_blank">here</a>.

There are two branches that get updated frequently, master and dev. The master branch will be considered stable, and will have features added between releases. The dev branch is considered unstable and this is where active developement happens.

Here's an example on how to add a call (call leg) to a coSpace using the module:

{ % gist b1f6fe180b831d18a89a % }

Then you can just run
<pre>Add-Participant -CoSpace df2d3e44-91ff-48f4-aeca-ffd951641ebe -SipUri anne.wallace@contoso.com</pre>
to add a participant.
