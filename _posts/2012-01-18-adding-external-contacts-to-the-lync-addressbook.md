---
layout: post
title: Adding external contacts to the #Lync addressbook
date: 2012-01-18 14:56
author: tomlarse
comments: true
categories: [Lync, powershell, Scripts, Unified Communications]
---
There are some scenarios where it would be nice to be able to add external contacts to the Lync addresse so that they are searchable for everyone in the organization. Or at least external in the sence that the contact has a sip domain that isn't supported in the Lync topology.

One such scenario could be an integration with an internal Cisco Telepresence solution.

The way to solve this is to add a contact object to AD that has the msRTCSIP-PrimaryUserAddress attribute populated, and the contact should be added to the address book on the next <a href="http://blog.schertz.name/2010/09/updating-the-lync-2010-address-book/" target="_blank">synchronization pass</a>. I've made a script to create this kind of object:

Note that displayName is not required, but if you don't add it the contact will only display the sipadress in the Lync client. I guess it's also possible to append other AD attributes to the user such as telephoneNumber.

I got a question about telephoneNumber as well, so I've added it as an optional parameter in the script.
Download latest version <a href="https://github.com/tomlarse/New-SipContact/releases/latest" target="_blank">here</a> - Contains both versions and an example .csv

Or copy the sourcecode:

```

#####################################################################################
 # New-SipContact.ps1
 #
 # Creates a contact object in AD that will be included in Lync/OCS address books.
 #
 #
 # Passing parameters:
 # .New-SipContact.ps1 -cn &quot;John Spencer&quot; -OUpath &quot;OU=SIPContacts,DC=contoso,DC=com&quot; -sipaddress &quot;john.spencer@litwareinc.com&quot; -displayname &quot;John Displayname Spencer&quot;
 #
 # Written by Tom-Inge Larsen (http://www.codesalot.com)
 #
 #####################################################################################
 param($cn,$OUpath,$sipAddress,$displayName=&quot;&quot;,$telephoneNumber=&quot;&quot;)

$fullpath= &quot;LDAP://&quot; + $OUpath
 $SIPContactOU = [ADSI]$fullpath

$SIPContact = $SIPContactOU.create(&quot;contact&quot;, &quot;cn=&quot; + $cn)
 $SIPContact.Put(&quot;Description&quot;,&quot;SIP Contact Object&quot;)
 $SIPContact.Put(&quot;msRTCSIP-PrimaryUserAddress&quot;, &quot;sip:&quot; + $sipAddress)
 if ($displayName -ne &quot;&quot;) {
 $SIPContact.Put(&quot;displayName&quot;, $displayName)
 }
 $SIPContact.Put(&quot;msRTCSIP-PrimaryUserAddress&quot;, &quot;sip:&quot; + $sipAddress)
 if ($telephoneNumber -ne &quot;&quot;) {
 $SIPContact.Put(&quot;telephoneNumber&quot;, $telephoneNumber)
 }
 $SIPContact.setInfo()
 ```

I've also created one to bulk create contacts from a .csv file

```

#####################################################################################
 # New-SipContactBulk.ps1
 #
 # Creates a contact object in AD that will be included in Lync/OCS address books.
 #
 #
 # Passing parameters:
 # .New-SipContactBulk.ps1 -OUpath &quot;OU=SIPContacts,DC=contoso,DC=com&quot; -csv &quot;c:newcontacts.csv&quot;
 #
 #
 # Written by Tom-Inge Larsen (http://www.codesalot.com)
 #
 #####################################################################################
 param($OUpath,$csv)

$fullpath= &quot;LDAP://&quot; + $OUpath
 $SIPContactOU = [ADSI]$fullpath

$contacts = Import-Csv -path $csv -header &quot;cn&quot;,&quot;displayName&quot;,&quot;sipaddress&quot;

foreach ($contact in $contacts) {

$SIPContact = $SIPContactOU.create(&quot;contact&quot;, &quot;cn=&quot; + $contact.cn)
 $SIPContact.Put(&quot;Description&quot;,&quot;SIP Contact Object&quot;)
 $SIPContact.Put(&quot;msRTCSIP-PrimaryUserAddress&quot;, &quot;sip:&quot; + $contact.sipaddress)
 if ($contact.displayname -ne &quot;&quot;) {
 $SIPContact.Put(&quot;displayName&quot;, $contact.displayName)
 }
 $SIPContact.setInfo()
 }

```

The example csv file contains this:

[sourcecode]
John Spencer,,john.spencer@litwareinc.com
Spencer John,Spencer Displayname John,spencer.john@litwareinc.com

```

