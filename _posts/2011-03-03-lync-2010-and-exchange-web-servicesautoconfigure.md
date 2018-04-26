title: Lync 2010 and Exchange Web Services/autoconfigure
link: http://blog.codesalot.com/2011/03/03/lync-2010-and-exchange-web-servicesautoconfigure/
author: tomlarse
description: 
post_id: 260
created: 2011/03/03 13:43:25
created_gmt: 2011/03/03 11:43:25
comment_status: open
post_name: lync-2010-and-exchange-web-servicesautoconfigure
status: publish
post_type: post

# Lync 2010 and Exchange Web Services/autoconfigure

I've recently been upgrading an OCS 2007 R2 environment to Lync 2010 where the users have SMTP adresses in several SMTP domains, but they only have one SIP domain. All users have an SMTP address at least in the SIP domain, but many of them have their primary SMTP address in different domains from the SIP domain.

## Comments

**[Chilly](#49 "2011-05-17 08:17:32"):** After LOTS of googling and searching, this is what finally got my Home Lab set up up and running fully, THANKS!

**[Leslin](#50 "2011-05-20 11:25:00"):** OK I have setup LYNC and it is working fine

**[tom](#51 "2011-05-20 11:43:52"):** Hi Leslin

**[AN](#52 "2012-01-24 22:56:35"):** Hi,

**[tom](#53 "2012-01-24 23:44:25"):** Hi AN

**[AN](#54 "2012-01-25 00:20:36"):** Hi Tom,

**[tom](#55 "2012-01-25 01:03:18"):** Ah, I see. If the clients are only internal, and you have control over internal DNS, you could try to create a split-brain DNS where you add the SRV records as their own zone in the internal DNS, like it's done in this [post](http://blogs.technet.com/b/dougl/archive/2009/06/12/communicator-automatic-configuration-and-split-brain-dns.aspx), only you add the SRVs for autodiscover instead of sipinternaltls.

**[AN](#56 "2012-01-25 15:19:29"):** Hi Tom,

