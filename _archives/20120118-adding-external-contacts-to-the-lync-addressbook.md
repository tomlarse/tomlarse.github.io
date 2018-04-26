title: Adding external contacts to the #Lync addressbook
link: http://blog.codesalot.com/2012/01/18/adding-external-contacts-to-the-lync-addressbook/
author: tomlarse
description: 
post_id: 364
created: 2012/01/18 14:56:24
created_gmt: 2012/01/18 12:56:24
comment_status: open
post_name: adding-external-contacts-to-the-lync-addressbook
status: publish
post_type: post

# Adding external contacts to the #Lync addressbook

There are some scenarios where it would be nice to be able to add external contacts to the Lync addresse so that they are searchable for everyone in the organization. Or at least external in the sence that the contact has a sip domain that isn't supported in the Lync topology.

## Comments

**[Jonas Mellquist](#66 "2012-02-08 12:47:49"):** Good stuff Tom-Inge

**[tom](#67 "2012-02-08 13:36:26"):** Great to be of any help :)

**[Rich](#126 "2012-08-24 22:06:51"):** Hey Tom, Good stuff. I need to get hold of the CSV file which doesn't appear to be linked correctly, could you fix that so I can grab it?

**[Matt](#288 "2013-07-11 06:21:00"):** Great script!

**[Tom-Inge Larsen](#289 "2013-07-11 09:30:02"):** Oops!

**[tomlarse](#127 "2012-08-29 08:21:40"):** Hey

**[Tom-Inge Larsen](#290 "2013-07-11 09:30:43"):** Hi,

**[Mitch](#251 "2013-06-20 23:39:15"):** How can I bulk edit existing contacts and add the msRTCSIP-PrimaryUserAddress? Another caveat is their SIP addresses do not match their email addresses.

**[Tom-Inge Larsen](#254 "2013-06-21 08:58:34"):** If it's not that many I guess the easiest would be to just use ADSI edit. If it is a lot of them it probably would be better to script it.

**[Michael Kjær](#269 "2013-07-01 11:25:00"):** Hi Tom, We have made contacts like this, for all of our video endpoints, and it Works great. To make it easier for our users, I wanted to ad a picture of a videoconferencing system to the contact's thumbnailphoto attribute, just like we do with all of our lync/Outlook users. However, I'm unable to make the picture show, when seaching from Lync.

**[Ashwin](#296 "2013-07-15 08:45:29"):** Thank you very much, great post!

**[Tom-Inge Larsen](#1552 "2014-06-03 09:50:51"):** Hi

**[Tom-Inge Larsen](#2054 "2014-08-26 18:59:58"):** Hi

**[Dave P](#2061 "2014-08-27 11:53:40"):** Ok thanks. Hoping some others on the thread may have some experience. So far, I've not had any success. I can see active Lync accounts associated with resource mailboxes (AD account enabled) in there, but not the contacts. Trying to figure out which bit makes it show up.

**[Dave P](#2010 "2014-08-21 19:30:27"):** This works great for Lync clients, but the contact or an existing Exchange resource that includes the msRTCSIP-PrimaryUser attribute doesn't show up in the address book on a Lync Room System. Is there another attribute we need to set for it to show up there? We have Lync Room System resource accounts that are Lync enabled show up in those contact lists.

**[Satya Prakash](#1545 "2014-06-02 11:23:10"):** Hi Tom,

**[swinster](#3906 "2015-07-30 10:52:04"):** Hey Tom/All,

**[swinster](#3850 "2015-07-12 23:40:36"):** Hi Tom,

**[swinster](#5010 "2017-05-02 16:37:53"):** FWIW, I this is supported in O365 or Hybrid models, which is a shame. You can, of course, create new "fake" AD users, but this might not be considered ideal. If anyone know any different, please let me know.

**[swinster](#3856 "2015-07-13 19:52:39"):** Ok, here is the sanitised script with modifications:

**[swinster](#3979 "2015-08-24 13:09:53"):** I think this is something you will have to do manually. There is an example CSV in Toms zip, but depending on what information you want to import, will depend on the headings you have in the CSV.

**[IcantfindtheCSVorExportit](#3964 "2015-08-21 01:03:34"):** How did you create the CSV? I dont know how to create the CSV :(

