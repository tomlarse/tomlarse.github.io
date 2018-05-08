---
layout: post
title: ! "Script: Find-CsLineUri"
date: 2013-10-07 10:58
author: tomlarse
comments: true
categories: [Lync, Lync 2010, Lync 2013, powershell, tools, Unified Communications]
---
Often I need to find a certain LineUri in Lync. LineUris are most of the time configured on users, so a simple

```
Get-CsUser -filter {LineUri -like &quot;tel:&lt;e164number&gt;*&quot;}
```


will give you the result you are looking for. But a user is not the only object in Lync that can have a LineUri, and if you in addition don't know what object has the LineUri you might need to search through all the objects. This script does just that. Sort of an opposite to Ståle Hansens <a href="http://msunified.net/lyncdownloads/script-list-unusednumbers-ps1/" title="list-unusednumbers" target="_blank">List-UnusedNumbers.ps1</a>.

The script will also list <span style="text-decoration:underline;">all</span> objects that have that LineUri, so it is useful in the situations where you have managed to get the same LineUri on two objects and are getting "SIP/2.0 485 Ambiguous" errors on calls. Normally, if you try to give an object a LineUri that is already configured it will throw a powershell error, but there are situations where it doesn't pick up on it, especially when using the ;ext=1234 addition to the LineUri.

<a href="http://codesalot.files.wordpress.com/2013/10/485.png"><img class="size-medium wp-image-536" alt="Lync reports a SIP 485 Ambiguous and a Diagnostic ID 4199 &quot;Multiple users associated with the target phone number&quot;" src="http://codesalot.files.wordpress.com/2013/10/485.png?w=300" width="300" height="26" /></a> Lync reports a SIP 485 Ambiguous and a Diagnostic ID 4199 "Multiple users associated with the target phone number"

Download <a href="http://codesalot.files.wordpress.com/2013/10/find-cslineuri.zip" title="Find-CsLineUri.zip" target="_blank">Find-CSLineUri.zip</a> or copy the sourcecode:

```
####################################################################################################
# Find-CsLineUri.ps1
#
# Lists all objects with a given LineUri
#
#
# Passing parameters:
# .\Find-CsLineUri.ps1 +4712345678
#
# Written by Tom-Inge Larsen (http://www.codesalot.com)
#
####################################################################################################
param($getlineuri)

Function ListContents
{
    Param($Heading,$list)

    Write-Host $Heading
    Write-Host &quot;--------------------------------------------------&quot;
    Write-Host

    foreach ($object in $list) {
       $object
    }
}

clear-host

write-debug $getlineuri

$getlineuri = &quot;tel:&quot; + $getlineuri + &quot;*&quot;

Write-debug $getlineuri

$csusers=Get-CsUser -Filter {LineURI -like $getlineuri} | Select-Object SipAddress,LineURI | out-string -stream
$csuserspl=Get-CsUser -Filter {PrivateLine -like $getlineuri} | Select-Object SipAddress,PrivateLine | out-string -stream
$csanalogs=Get-CsAnalogDevice -Filter {LineURI -like $getlineuri} | Select-Object SipAddress,LineURI | out-string -stream
$cscaps=Get-CsCommonAreaPhone -Filter {LineURI -like $getlineuri} | Select-Object SipAddress,LineURI | out-string -stream
$csums=Get-CsExUmContact -Filter {LineURI -like $getlineuri} | Select-Object SipAddress,LineURI | out-string -stream
$csdialins=Get-CsDialInConferencingAccessNumber -Filter {LineURI -like $getlineuri} | Select-Object PrimaryUri,LineURI | out-string -stream
$cstrusteds=Get-CsTrustedApplicationEndpoint -Filter {LineURI -like $getlineuri} | Select-Object SipAddress,LineURI | out-string -stream
$csrgses=Get-CsRgsWorkflow | Where-Object {$_.LineUri -like $getlineuri} | Select-Object PrimaryUri,LineURI | out-string -stream

if ($csusers -ne $null){ListContents -Heading &quot;User&quot; -list $csusers}
if ($csuserspl -ne $null){ListContents -Heading &quot;Private Line&quot; -list $csuserspl}
if ($csanalogs -ne $null){ListContents -Heading &quot;Analog Device&quot; -list $csanalogs}
if ($cscaps -ne $null){ListContents -Heading &quot;Common Area Phone&quot; -list $cscaps}
if ($csums -ne $null){ListContents -Heading &quot;Exchange UM Contact&quot; -list $csums}
if ($csdialins -ne $null){ListContents -Heading &quot;Dial-in Conference Number&quot; -list $csdialins}
if ($cstrusteds -ne $null){ListContents -Heading &quot;Trusted Application Endpoint&quot; -list $cstrusteds}
if ($csrgses -ne $null){ListContents -Heading &quot;Response Group Workflow&quot; -list $csrgses}
```
