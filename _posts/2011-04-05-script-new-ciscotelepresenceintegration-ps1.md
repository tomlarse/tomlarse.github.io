---
layout: post
title: Script - New-CiscoTelepresenceIntegration.ps1
date: 2011-04-05 10:44
author: tomlarse
comments: true
categories: [Cisco Telepresence, Lync, powershell, Unified Communications]
---
Script to enable routes from Lync to VCS Control: ---- Edit: After the VCS X7 release, the integration is done a bit differently. I'll try to get an update to the script out in the near future.

[sourcecode language="powershell"]
######################################################################################################################################################################################
# New-CiscoTelepresenceIntegration.ps1
#
# Adds config in Lync 2010 for integration with Cisco Telepresence (Tandberg)
#
# Can optionally write logs to file or screen using -verbose and/or -logFile inputs
#
# eg.
# Clean Lync installation
# .New-CiscoTelepresenceIntegration.ps1 -vcscfqdn vcsc011.contoso.com -lsfepool lspool01.contoso.com -CTPSipDomain video.contoso.com -logFile &quot;c:logfile.txt&quot;
#
# Coexisting with OCS 2007 R2
# .New-CiscoTelepresenceIntegration.ps1 -coexistence $true -r2pool r2pool01.contoso.com -lsfepool lspool01.contoso.com -CTPSipDomain video.contoso.com -logFile &quot;c:logfile.txt&quot;
#
# Migration from OCS 2007 R2 to Lync
# .New-CiscoTelepresenceIntegration.ps1 -hascoexisted $true -vcscfqdn vcsc011.contoso.com -lsfepool lspool01.contoso.com -CTPSipDomain video.contoso.com -logFile &quot;c:logfile.txt&quot;
#
# Important:
# This will delete any existing static routes created ! Do not run the script with hascoexisted = $true if you have added manual routes other than OCS/Lync/CTP integration
#
# Written by Tom-Inge Larsen (&lt;a href=&quot;http://www.codesalot.com&quot;&gt;www.codesalot.com&lt;/a&gt;), Peder Saether and Trond Egil Gjelsvik-Bakke
# Based on config made by Marjus Sirvinsks (marjuss.wordpress.cm)
#
#######################################################################################################################################################################################
param($logFile,$coexistence=$false,$hascoexisted,$CTPSipDomain,$lsfepool,$r2pool,$vcscfqdn)&lt;/pre&gt;
if ($logFile -ne $null) {
$a = &quot;Steps made to enable integration with Cisco Telepresence: `n&quot;
Out-File -FilePath $logfile -InputObject $a
}

if ($lsfepool -eq $null) {
$lsfepool = Read-Host &quot;Please enter Lync Front End pool FQDN.&quot;
}

if ($CTPSipDomain -eq $null) {
$CTPSipDomain = Read-Host &quot;Please enter the SIP domain in the Cisco Telepresence environment.&quot;
}

if ($coexistence -eq $false) {
#Change encryption level if SRTP option is not available for VCS
$mediaconfiguration = get-csmediaconfiguration
$requireencryption = ($mediaconfiguration.EncryptionLevel -eq &quot;RequireEncryption&quot;)
if ($requireencryption) {
write-warning &quot;This will set the media encryption level to Support Encryption. Are you sure you want to do this? (y/n)&quot;
$confirmation = Read-Host

} else {
$confirmation = 'y'
}
switch ($confirmation) {
'y' {
set-CsMediaConfiguration -EncryptionLevel supportencryption

$registrarid = &quot;service:registrar:&quot;+$lsfepool
$trustedappregistrar = &quot;Registrar:&quot;+$lsfepool

if ($hascoexisted -eq $true) {
Remove-CsStaticRoutingConfiguration -Identity $registrarid
}

if ($vcscfqdn -eq $null) {
$vcscfqdn = Read-Host &quot;Please enter the FQDN for the VCS Control&quot;
}

#Establish trust
$applicationpooladded = $true
New-CsTrustedApplicationPool -Identity $vcscfqdn -Registrar $trustedappregistrar -site 1 -RequiresReplication $false -ThrottleAsServer $true -TreatAsAuthenticated $true -force

New-CsTrustedApplication -ApplicationID &quot;CiscoTelepresenceDirectSIP&quot; -TrustedApplicationPoolFqdn $vcscfqdn -Port 5061

#Create static routes if needed

if ($hascoexisted -eq $true) {
New-CsRegistrarConfiguration -Identity $registrarid
}

New-CsStaticRoutingConfiguration -identity $registrarid

$route = New-CsStaticRoute -TLSRoute -destination $vcscfqdn -port 5061 -matchuri $CTPSipDomain -usedefaultcertificate $true

Set-CsStaticRoutingConfiguration -identity $registrarid -route @{Add=$route}

Enable-CsTopology
}
'n' {
Write-Warning &quot;No change was made to the topology. Media Encryption Level must be set to Support Encryption&quot;
if ($logFile -ne $null) {
$a = &quot;No change has been made. `n&quot;
Out-File -FilePath $logfile -InputObject $a -Append
}
}
}
}

else {

# If we coexist with R2, we might want to route all traffic via R2 FE, to possibly avoid
# compromising security with deployments using TCP or if Lync is only intended as a
# pilot.

if ($r2pool -eq $null) {
$r2pool = Read-Host &quot;Please enter OCS 2007 R2 Front End pool FQDN.&quot;
}

$registrarid = &quot;service:registrar:&quot;+$lsfepool

New-CsRegistrarConfiguration -Identity $registrarid
New-CsStaticRoutingConfiguration -identity $registrarid

$route = New-CsStaticRoute -TLSRoute -destination $r2pool -port 5061 -matchuri $CTPSipDomain -usedefaultcertificate $true
Set-CsStaticRoutingConfiguration -identity $registrarid -route @{Add=$route}

Enable-CsTopology
}

if ($logFile -ne $null) {

$a = &quot;Route added: `n&quot;
Out-File -FilePath $logfile -InputObject $a -Append
Get-CsStaticRoutingConfiguration $registrarid | Select-Object -ExpandProperty Route | Where-Object {$_.MatchUri -eq $CTPSipDomain} | Out-File -FilePath $logfile -Append
if ($applicationpooladded -eq $true){
$a = &quot;`nTrusted Application Pool added:`n&quot;
Out-File -FilePath $logfile -InputObject $a -Append
Get-CsTrustedApplicationPool $vcscfqdn | Out-File $logfile -append
}
$a = &quot;`nRegistrar added:`n&quot;
Out-File -FilePath $logfile -InputObject $a -Append
Get-CsStaticRoutingConfiguration $registrarid | Out-File $logFile -append

if ($confirmation -eq 'y') {
$a = &quot;`nMedia encryption level was already set to or was set to Support Encryption.`n&quot;
Out-File -FilePath $logfile -InputObject $a -Append
}

Write-Host &quot;Logfile: &quot; $logFile &quot;is written.&quot;
}
[/sourcecode]
