---
layout: post
title: Disable AD disabled CS users powershell script
date: 2011-03-10 17:13
author: tomlarse
comments: true
categories: [automation, Lync 2010, powershell, script, Scripts, Unified Communications, usermanagement]
---
I've made a script to disable AD disabled users from Lync. The script pulls all AD disabled users and checks if they are disabled for Lync as well. If not, they will be. Optional output to screen and/or file.

Download <a href="http://codesalot.files.wordpress.com/2011/03/disable-addisabledcsusers.zip">Disable-AdDisabledCsUsers.zip</a> or copy the sourcecode:
<div>[sourcecode language="powershell"]
 #####################################################################################
 # Disable-AdDisabledCsUsers.ps1
 #
 # Pulls all AD disabled users from AD and disables them for Lync as well
 #
 # Can optionally write logs to file or screen using -verbose and/or -logFile inputs
 #
 # eg.
 #
 # .Disable-AdDisabledCsUsers.ps1 -verbose $true -logFile &quot;c:logfile.log&quot;
 #
 #
 #
 # Written by Tom-Inge Larsen (codesalot.com)
 #
 ####################################################################################
 param($verbose,$logFile)
Import-Module active*&lt;/code&gt;&lt;/code&gt;if ($logFile -ne &quot;&quot;) {
 $logoutput = [System.IO.StreamWriter] $logFile
 $logoutput.WriteLine(&quot;AD disabled users that was Lync disabled:&quot;)
 }

$disabledADusers = Search-ADAccount -AccountDisabled -UsersOnly | Select-Object userprincipalname

$disabledADusers | foreach-object {
 $identity = $_.userprincipalname
 $csuser = Get-CsUser -Identity $identity -ErrorAction SilentlyContinue | Select-Object Enabled

if ($csuser.enabled -eq $true) {
 Disable-CsUser -Identity $identity
 if ($verbose -eq $true) {
 Write-Host &quot;AD disabled user&quot; $identity &quot;is now disabled for Lync as well&quot;
 }
 if ($logFile -ne &quot;&quot;) {
 $logoutput.WriteLine($identity)
 }
 }
 }

if ($logFile -ne &quot;&quot;) {
 $logoutput.close()
 if ($verbose -eq $true) {
 Write-Host $logFile &quot;written.&quot;
 }
 }

[/sourcecode]

</div>
