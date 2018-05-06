---
layout: post
title: Error when moving user from Skype4B onprem to online
date: 2016-08-09 10:18
author: tomlarse
comments: true
categories: [Uncategorized]
---
In a freshly set up Skype for Business hybrid environment we got this error after trying to move the first user from onprem to online:
<blockquote>HostedMigration 510 error : the user could not be moved because the tenant has not been enabled for shared SIP address spaces</blockquote>
After verifying that both the tenant and onprem environment is actually set up for shared address spaces with

```
Get-CsTenantFederationConfiguration
```

and

```
Get-CsHostingProvider
```

the issue is still there.

I did find a <a href="http://blankmanblog.com/general-news/tips-tricks/hostedmigration-510-error-the-user-could-not-be-moved-because-the-tenant-has-not-been-enabled-for-shared-sip-address-spaces/" target="_blank">blogpost </a>and <a href="http://answers.microsoft.com/en-us/msoffice/forum/msoffice_o365admin-mso_manage/hostedmigration-510-error-the-user-could-not-be/23d6a7e9-81a9-4f13-a2ad-49c6776bebf0?auth=1" target="_blank">an ms forum post</a> on this, but in both those cases the problem seemed to be some caching of some sort and solved itself, which it didn't in my scenario.

It turned out that the user were homed in a child domain and the FE pool in the root domain. The problem was solved by running the Move-CsUser Cmdlet with the -DomainController parameter as well, like this:

```
Move-CsUser -Identity user@contoso.com -Target sipfed.online.lync.com -Credential $cred -HostedMigrationOverrideUrl &quot;https://adminXX.online.lync.com/HostedMigration/hostedmigrationService.svc&quot; -DomainController dc.contoso.com
```

Remember that your HostedMigrationOverrideUrl will probably be different, just log in to the SFBO admin portal to get yours.´´´
