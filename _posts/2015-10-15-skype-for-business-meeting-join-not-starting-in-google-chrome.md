---
layout: post
title: Skype for Business meeting join not starting in Google Chrome
date: 2015-10-15 13:21
author: tomlarse
comments: true
categories: [Chrome, Lync, meetings, Skype for Business, Unified Communications]
---
Today I got to troubleshoot this little curiosity. A customer that uses Google Chrome as their standard browser reported that a few of their users wasn't able to join meetings when clicking the meeting join link, nothing happens and they are displayed a page looking like this.

<a href="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-15-46.png"><img class="alignnone wp-image-648 size-large" src="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-15-46.png?w=660" alt="2015-10-15_14-15-46" width="660" height="340" /></a>

When a user joins a Skype for Business or Lync meeting for the first time in Chrome, they are presented with this message:

<img class="alignnone wp-image-651 size-full" src="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-14-31.png" alt="2015-10-15_14-14-31" width="448" height="377" />

What probably had happened to those users is that they have checked "Remember my choice for all links of this type." and then clicked "Do Nothing".

<img class="alignnone size-full wp-image-652" src="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-14-52.png" alt="2015-10-15_14-14-52" width="448" height="377" />

What this will do is that Chrome will block URLs trying to launch the Skype for Business or Lync client using the lync15: protocol, rendering the browser unable to launch the client and forcing the user to use the web app.

Removing this block isn't very hard, but as far as I know it is not accessible from any part of the Chrome GUI. Here's what you need to do:
<ol>
	<li>Open %userprofile%\AppData\Local\Google\Chrome\User Data on the users computer</li>
	<li>Locate the file "Local State" and open it in notepad</li>
	<li>Locate the "protocol_handler" directive in the file and find "lync15:" under it
<a href="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-24-02.png"><img class="alignnone size-large wp-image-653" src="https://codesalot.files.wordpress.com/2015/10/2015-10-15_14-24-02.png?w=660" alt="2015-10-15_14-24-02" width="660" height="264" /></a></li>
	<li>If "Lync15:" is followed by "true", it means that the protocol is blocked, and the client won't be launched.</li>
	<li>To resolve the issue, either
<ol>
	<li>remove the whole ""lync15:":true," (including the last comma). This will reset the configuration, and the user will be presented with the above dialogue again the next time they try to join a meeting, giving them another opportunity to block the protocol</li>
	<li>replace "true" with "false", which will unblock the protocol.</li>
</ol>
</li>
</ol>
