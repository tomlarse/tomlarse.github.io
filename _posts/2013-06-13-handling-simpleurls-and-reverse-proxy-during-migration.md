---
layout: post
title: Handling SimpleURLs and Reverse Proxy during migration
date: 2013-06-13 10:39
author: tomlarse
comments: true
categories: [Certificates, DNS, Lync, Lync 2010, Lync 2013, Migration, Reverse Proxy, SimpleURL, Unified Communications]
---
I've thought about writing this post for a while, as the topic isn't really covered very well in the Lync 2013 <a href="http://technet.microsoft.com/en-us/library/jj205369.aspx" target="_blank">migration documentation</a>. The issue is also only relevant when migrating from Lync 2010 to Lync 2013.

The scenario is this: You are doing a migration from Lync 2010 to Lync 2013. You are following the migration steps provided in the migration documentation, and have planned and prepared your migration, deployed a pilot pool and moved some pilot users to Lync 2013. Internally everything is working as it should,  all modalities are working and conferencing works via the meeting join page using simple urls regardless of which server the user is on.

Now, most of the deployments I do are not large enough that it is needed to use more than one FE pool and for external access one Edge pool and one reverse Proxy. Because of this, most of the conferencing going on is involving external participants. This means that modalities and meeting join needs to be working for the pilots in external scenarios as well. The next step in the migration documentation covers some of this with the deployment of the Edge server. This will handle the peer to peer modalities, but what about the simple URLs?

If you try to reuse the existing reverse proxy rules, you will end up in one of these situations:
<ol>
	<li><strong>You keep the rule as it is, pointing toward the Lync 2010 pool</strong>
If you do this, simple URLs and meeting join will continue working for meetings created by the Lync 2010 users. But if someone external tries to join a meeting created by one of the pilot Lync 2013 users, they will be met with a page saying "Sorry, something went wrong, and we can't get you into the meeting." and if you click on "more info" you will get en error saying "Error:Invalid Conference organizer or Conference ID" like this:
<a href="http://codesalot.files.wordpress.com/2013/06/meetingjoinerror.png"><img class="alignnone size-medium wp-image-500" alt="meetingjoinerror" src="http://codesalot.files.wordpress.com/2013/06/meetingjoinerror.png?w=272" width="272" height="300" /></a>
The Lync 2013 pilot users will also not be able to log in via the mobile client.</li>
	<li><strong>You change the rule, pointing it toward the new Lync 2013 pool</strong>
If you do this, everyting will work as it should for the Lync 2013 users. But if someone tries to join a meeting created by one of the Lync 2010 users, they will be met with an ordinary IIS "404 not found" page
<a href="http://codesalot.files.wordpress.com/2013/06/404.png"><img class="alignnone size-medium wp-image-501" alt="404" src="http://codesalot.files.wordpress.com/2013/06/404.png?w=300" width="300" height="109" /></a></li>
</ol>
Both of these solutions are not really wanted in a normal migration, so what do we do then? The solution is to handle it as a normal multiple pool deployment. This is as it turns out not really well documented in the TechNet library, but on the <a href="http://technet.microsoft.com/en-us/library/gg429704.aspx" target="_blank">Request and Configure a Certificate for Your Reverse HTTP Proxy</a> page there is a note saying this:

<em>If your internal deployment consists of more than one Standard Edition server or Front End pool, you must configure web publishing rules for each external web farm FQDN and you will either need a certificate and web listener for each, or you must obtain a certificate whose subject alternative name contains the names used by all of the pools, assign it to a web listener, and share it among multiple web publishing rules.</em>

This means that you will need to deploy a new reverse proxy publishing rule for the new Lync 2013 Pool with a different DNS name for the external services. The rule will also need to use a certificate that contains all the simple URL names in addition to the new name for the external web services and lyncdiscover. This will in most cases create a need for a new public certificate for this new rule.

By doing this Lync is able to redirect the traffic to the webservices between the reverse proxy rules as it does on the inside, and all functionality should be available for both existing Lync 2010 users and the Lync 2013 pilot users.
