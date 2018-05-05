---
layout: post
title: Lync Meetings and Transport Neutral Encapsulation Format
date: 2014-05-23 09:52
author: tomlarse
comments: true
categories: [Exchange, Lync, Lync Meeting, Lync Room System, Meeting Invitations, TNEF, Unified Communications, video conferencing]
---
One of the small things that make Lync Meetings so simple to join is that Outlook will recognize the meeting and wil give you a small button on the Outlook reminder that lets you join the meeting without even opening the calendar. This is also the same functionality that clickable from the calendar interface on the mobile and desktop clients and makes the meeting joinable from a Lync Room System.

[gallery type="rectangular" ids="558,559,556" orderby="rand"]

Some might have noticed though that when the Lync meeting invites come from an external organization, none of the clients will actually recognize the meeting as a Lync meeting. For most of the clients this is not a big problem, because the link in the invite will still be clickable, but for the Lync Room System this will actually render the meeting unjoinable.

The method that is beeing used in the meeting invites to identify a calendar object as a Lync meeting is called <a href="http://en.wikipedia.org/wiki/Transport_Neutral_Encapsulation_Format" target="_blank">Transport Neutral Encapsulation Format, or TNEF</a>. TNEF is basically an attachment format that is used by Outlook and Exchange in different situations additional formatting is needed, like voting and meeting invites.

The global settings for sending TNEF to remote domains is default set to false. This means that when sending Lync Meeting invites out of the organization, the TNEF attachment is stripped off and the recieving party does not get the extra data which in turn makes the Lync clients at the recieving party not recognize the meeting as a Lync meeting.

To resolve this, the sending party needs to enable sending of TNEF attachments to the recieving party. This is done via the RemoteDomain settings, and can be turned on for i.e contoso.com like this:

[sourcecode language="powershell"]
New-RemoteDomain -DomainName contoso.com -Name Contoso
Set-RemoteDomain -Identity Contoso -TNEFEnabled $true
[/sourcecode]

It is also possible to set TNEF on for all remote domains, but be careful with this as TNEF can cause issues if the recieving end does not use Exchange.
