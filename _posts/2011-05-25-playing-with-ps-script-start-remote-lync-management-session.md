---
layout: post
title: ! "Playing with PS: Script: Start remote Lync management session"
date: 2011-05-25 15:21
author: tomlarse
comments: true
categories: [Lync, RBAC, script, Unified Communications]
---
I wrote a script to start a remote Lync management shell session based on <a href="http://blogs.technet.com/b/csps/archive/2010/06/16/qsremoteaccess.aspx">this</a> post. This of course is a big bloated way to do it (it can be done as a <a href="http://blog.powershell.no/2010/12/05/lync-server-2010-remote-administration/">twoliner</a>), but I need the PS training :P

```
 ##########################################################################################################################
 # New-RemoteCSPSsession.ps1
 #
 # Opens a remote session to a Lync Management Shell and imports all commands
 #
 # Uses current logged inn credentials, but can optionally supply other credentials.
 #
 # eg.
 # Prompt for fefqdn:
 # .New-RemoteCSPSsession.ps1
 #
 # Use other credential:
 # .New-RemoteCSPSsession.ps1 -othercredential $true
 #
 # Ignore certificates on fe:
 # .New-RemoteCSPSsession.ps1 -notrust $true
 #
 # fefqdn can be passed in arguments as well:
 # .New-RemoteCSPSsession.ps1 -csfe lync-admin.contoso.local
 #
 # Written by Tom-Inge Larsen (www.codesalot.com), based on this blogpost:
 # (http://blogs.technet.com/b/csps/archive/2010/06/16/qsremoteaccess.aspx)
 # this script can also easily be run as a twoliner:
 # (http://blog.powershell.no/2010/12/05/lync-server-2010-remote-administration/)
 #
 # $session = New-PSSession -ConnectionUri https://lync-admin.contoso.local/OcsPowershell -Credential (Get-Credential)
 # Import-PSSession -Session $session
 #
 #
 ##########################################################################################################################
 param($othercredential,$notrust,$csfe)

$env = get-host
 $majorversion = $host.version.major

if ($majorversion -lt 2) {
 write-Host &quot;You need to run at least Powershell 2.0 to run this script. http://support.microsoft.com/kb/968929&quot;
 } else {

if ($csfe -eq $null) {
 $csfe = Read-Host &quot;Please enter the FQDN of the Lync Front End pool you want to connect to&quot;
 }

$connectionURI = &quot;https://&quot;+$csfe+&quot;/OcsPowershell&quot;
 $cmdstring = 'New-PSSession -ConnectionUri $connectionURI'

if ($othercredential -eq $true) {
 $credential = Get-Credential
 $cmdstring += ' -Credential $credential'
 }
 if ($notrust -eq $true) {
 $sessionoption = New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck
 $cmdstring += ' -SessionOption $sessionoption'
 }

$session = &amp; $executioncontext.invokecommand.NewScriptBlock($cmdstring)

Import-PSSession $session
 }

```
