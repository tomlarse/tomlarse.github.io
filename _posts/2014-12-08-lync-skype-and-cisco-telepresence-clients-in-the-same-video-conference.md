---
layout: post
title: Lync, Skype and Cisco Telepresence clients in the same video conference!
date: 2014-12-08 09:01
author: tomlarse
comments: true
categories: [Cisco Telepresence, Lync, Lync Client, Skype, Unified Communications, video conferencing]
---
Late afternoon last Friday (In europe at least :)), Microsoft released video calling between Lync and Skype. This has been something that a lot of us has been waiting for for quite some time! You can read more about this release <a title="here" href="http://blogs.office.com/2014/12/05/video-calling-skype-lync-available-now/" target="_blank">here.</a>

To be able to video call a Lync contact from Skype, and vice versa, the following needs to be set up:
<ul>
	<li>The Lync environment needs to be federated wi<a href="https://codesalot.files.wordpress.com/2014/12/lyncoptions.png"><img class=" size-medium wp-image-579 alignright" src="https://codesalot.files.wordpress.com/2014/12/lyncoptions.png?w=300" alt="lyncoptions" width="300" height="238" /></a>th Skype - see the <a href="http://technet.microsoft.com/en-us/library/dn440173.aspx" target="_blank">Provisioning Guide</a></li>
	<li>The Lync user needs to use the Lync 2013 client.</li>
	<li>The Lync user has to be enabled for Public Access, and will have to set "Contacts not using Lync" to "Allow invites but block all other communications" or "Allow anyone to contact me" under "Alerts" in the Lync options menu.</li>
	<li>If set to "Allow invites but block all other communications" both the Lync user and the Skype user must add each other to their contact lists</li>
	<li>Currently it will only work from Skype on a Windows desktop running at least version 7.0.x.100. More Skype clients will be supported in the coming months.</li>
</ul>
This also brings cool opportunities when using Lync together with for instance <a href="http://acano.com/">Acano</a> or <a href="http://pexip.com/" target="_blank">Pexip </a>MCU software. This screenshot is from a video conference using the Acano brigde, and here is a Skype Client, a Lync Client and a Lync mobile Client brought together with a Cisco Telepresence room! Pretty awesome! The screenshot is taken from the Skype Client.<a href="https://codesalot.files.wordpress.com/2014/12/lyncskypeciscotp.png"><img class="aligncenter wp-image-581 size-large" src="https://codesalot.files.wordpress.com/2014/12/lyncskypeciscotp.png?w=625" alt="lyncskypeciscotp" width="625" height="402" /></a>

&nbsp;
