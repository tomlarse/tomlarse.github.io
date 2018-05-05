---
layout: post
title: Provision phonebook in Tandberg Management Suite
date: 2009-08-12 14:59
author: tomlarse
comments: true
categories: [Movi2, Provisioning, Tandberg, TMS, video conferencing]
---
To be able to add Movi2 endpoints to phonebooks on systems registered in TMS, TMS should automagically create an external source and a provisioning phonebook when the provisioning key is installed on the system. If this for some reason does not happen, here's how to add one: (or to verify that the phonebook was installed correctly)

In TMS, go to: <strong>Phone Book &gt; Manage External Source</strong>

If there is an external source there that is called "Provisioning Source", chances are that the phone book was installed correctly. If not, add a new external source and select "TANDBERG Provisioning Directory" as source type.

The rest of the fields should be like this:
<table border="1" cellspacing="0" cellpadding="0" width="744">
<tbody>
<tr>
<td colspan="2" width="744" valign="top"><strong><em>Connection Details </em></strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Name </strong></td>
<td width="331" valign="top"><strong>Provisioning Source </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Default Bandwidth for Imported Entries </strong></td>
<td width="331" valign="top"><strong>384 kbps </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Force Default Bandwidth (all entries, not only Auto entries) </strong></td>
<td width="331" valign="top">Unchecked</td>
</tr>
<tr>
<td width="413" valign="top"><strong>IP Address/DNS </strong></td>
<td width="331" valign="top"><strong>localhost </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Username </strong></td>
<td width="331" valign="top"><strong>CN=Directory Manager </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Password </strong></td>
<td width="331" valign="top"><strong>TANDBERG </strong></td>
</tr>
<tr>
<td colspan="2" width="744" valign="top"><strong><em>Advanced Connection   Details </em></strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>LDAP Port Number </strong></td>
<td width="331" valign="top">Blank</td>
</tr>
<tr>
<td width="413" valign="top"><strong>Search Base (DN) </strong></td>
<td width="331" valign="top"><strong>dc=provisioning </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Search Scope </strong></td>
<td width="331" valign="top"><strong>Recursive </strong></td>
</tr>
<tr>
<td width="413" valign="top"><strong>Custom LDAP Filter </strong></td>
<td width="331" valign="top">Blank</td>
</tr>
<tr>
<td width="413" valign="top"><strong>Field on User Object to Prefix Display Name in TMS </strong></td>
<td width="331" valign="top"><strong>displayName </strong></td>
</tr>
</tbody></table>
With this setup, movi users are added to the phone book on the format "&lt;firstname&gt; &lt;lastname&gt; &lt;provisioningprofile&gt;". I will try some different settings to see if I can filter and change the format in the phonebook. I will add this in a later post.

After this, create a new phonebook and connect it to the new external source.

Source: Tandberg Deployment guide: Provisioning. february 2009
<div id="_mcePaste" style="overflow:hidden;position:absolute;left:-10000px;top:97px;width:1px;height:1px;">Connection Details
Name
Provisioning Source
Default Bandwidth for Imported Entries
384 kbps
Force Default Bandwidth (all entries, not only Auto entries)
Unchecked
IP Address/DNS
localhost
Username
CN=Directory Manager
Password
TANDBERG
Advanced Connection Details
LDAP Port Number
Blank
Search Base (DN)
dc=provisioning
Search Scope
Recursive
Custom LDAP Filter
Blank
Field on User Object to Prefix Display Name in TMS
displayName</div>
