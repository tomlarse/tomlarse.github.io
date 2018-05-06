---
layout: post
title: Desktop sharing issues with Palo Alto firewalls
date: 2015-09-28 08:14
author: tomlarse
comments: true
categories: [desktop sharing, firewall traversal, Lync, Skype for Business, Unified Communications]
---
Earlier this year we were contacted by several customers reporting desktop sharing issues in scenarios involving participants on the outside of the firewall. These users fall in to two categories
<ul>
	<li>Users belonging to the organization that are logged inn via the edge server - Edge server users</li>
	<li>Users not belonging to the organization - Federated users</li>
</ul>
The symptoms they experienced were all the same
<ul>
	<li>Desktop sharing fails intermittently in the following scenarios
<ul>
	<li>One to one between federated and user logged in directly on FE</li>
	<li>Fails for external users in both categories when participating in conferences</li>
</ul>
</li>
</ul>
If we look at the Desktop Sharing page in the <a href="http://www.microsoft.com/en-us/download/details.aspx?id=46448" target="_blank">Skype for Business Protocol Workloads</a> poster, we can see where the media is supposed to flow in these scenarios

<a href="https://codesalot.files.wordpress.com/2015/09/untitled-picture.png"><img class="alignnone size-large wp-image-639" src="https://codesalot.files.wordpress.com/2015/09/untitled-picture.png?w=660" alt="Untitled picture" width="660" height="398" /></a>

When a federated user or a conference is involved, the media is sent through TCP via the AVMCU on the edge server. So the issue seems to be with the outbound TCP 50000-59999 port range traversing the firewall.

The call fails with the following reason in the BYE:
<pre style="margin:0;font-family:Calibri;font-size:11pt;">Ms-client-diagnostics: 23; reason="Call failed to establish due to a media connectivity failure when one endpoint is internal and the other is remote"´´´
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">The ICE warning is 0x8000100, which if looked up in the Reskit documentation or the <a href="https://gallery.technet.microsoft.com/office/ICE-Warning-Flag-Decoder-97058ef3" target="_blank">ICE Warning Flags decoder</a>, means this</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>

<pre style="margin:0;font-family:Calibri;font-size:11pt;"><strong>TCP NAT connectivity failed
</strong>This flag is expected. If local-to-local connectivity succeeded, the TCP NAT connectivity check may not have been tried. Or there is no direct TCP connection possible.
TCP NAT connectivity failing may result in an ICE protocol failure.´´´
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">Another clue pointing to the TCP media port range.</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">We also saw a lot of TCP retransmits when doing packet tracing, the edge server was not happy with the TCP connection when trying to set up the desktop sharing session.</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">What we realised fairly early was that all customers reporting this was running Palo Alto firewalls, which tries to look at what kind of application the traffic is in stead of the traditional just looking at port numbers.</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">After quite a bit of troubleshooting - everything was set up by the book, nothing seemed to be wrong other than the media failing - we were able to make a case with Palo Alto support, and it eventually turned out to be a bug in the Palo Alto software that doesn't recognize the desktop sharing session as that, but tries to decrypt the session - even if no decryption is configured anywhere else on the firewall. The bug was as far as we can tell introduced in version 6.1.3, and has been reported fixed in an upcoming version 7.0.3. PAN support gave this workaround:</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><strong>Create a custom application for port 443</strong></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><a href="https://codesalot.files.wordpress.com/2015/09/customapp.png"><img class="alignnone size-large wp-image-642" src="https://codesalot.files.wordpress.com/2015/09/customapp.png?w=660" alt="customapp" width="660" height="25" /></a></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><strong>Create an application override for port 443</strong></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><a href="https://codesalot.files.wordpress.com/2015/09/appoverride.png"><img class="alignnone size-large wp-image-643" src="https://codesalot.files.wordpress.com/2015/09/appoverride.png?w=660" alt="appoverride" width="660" height="34" /></a></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><strong>Create a policy</strong></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"><a href="https://codesalot.files.wordpress.com/2015/09/policy.png"><img class="alignnone size-large wp-image-644" src="https://codesalot.files.wordpress.com/2015/09/policy.png?w=660" alt="policy" width="660" height="25" /></a></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
<p style="margin:0;font-family:Calibri;font-size:11pt;">This has solved the issue for us.</p>
<p style="margin:0;font-family:Calibri;font-size:11pt;"></p>
