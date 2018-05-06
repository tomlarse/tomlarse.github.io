---
layout: post
title: List static routing config
date: 2011-05-26 09:51
author: tomlarse
comments: true
categories: [Lync, powershell, Unified Communications]
---
<div>After adding a static route to Lync (for example when adding a <a href="http://www.codesalot.com/2011/script-new-ciscotelepresenceintegration-ps1/">CTP integration</a>) you can use the following command to show the route:</div>

```
 Get-CsStaticRoutingConfiguration Service:Registrar:lspool01.contoso.com
 ```

´´´Identity : Service:Registrar:lspool01.contoso.com
Route    : {MatchUri=video.contoso.com;MatchOnlyPhoneUri=False;Enabled=True;ReplaceHostInRequestUri=False}´´´
This will list the static route, but it won't show all the route details (specifically the route target which is semi often used in troubleshooting) as they are contained inside a Route object in the StaticRoutingConfiguration object. To list the details of the route, do:

https://gist.github.com/tomlarse/b8974b83625445b4060e

This will give you the content of the route.
´´´Transport               : TransportChoice=Certificate=Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.UseDefaultCert;Fqdn=<span style="color:#ff0000;">vcsc.contoso.com</span>;Port=5061
MatchUri                : video.contoso.com
MatchOnlyPhoneUri       : False
Enabled                 : True
ReplaceHostInRequestUri : False´´´
