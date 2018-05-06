---
layout: post
title: Integrating Acano callbridge with more than one Skype for Business Front End pool
date: 2016-04-21 16:47
author: tomlarse
comments: true
categories: [Uncategorized]
---
When integrating an Acano callbridge with Skype for Business (or any of the Lync versions), one of the tasks needed is to provide the callbridge with one or more SfB-enabled users that it can use to obtain MRAS credentials so that it can send media through the SfB edge server to external SfB users. This user is also used by the callbridge to look up SfB conference ID's when using multi-homed conferencing.

This is normally configured in the webadmin under the "Lync Edge settings" heading, found under Configuration-&gt;General. Funnily enough, none of these settings actually reference the edge servers in any way, the callbridge registers this (these) user(s) to the front end pool and is provided with the MRAS URI (basically the SfB edge TURN credentials) during the registration process.

<img class="alignnone size-full wp-image-842" src="https://codesalot.files.wordpress.com/2016/04/untitled-picture.png" alt="Untitled picture" width="842" height="163" />

The "Number of registrations" field dictates how many users the server will register, you need one for every 12 simultaneous calls you need to support through the SfB edge. If this is set to one the server will register the sip address configured in the username field, if it is set to a number greater than 1 it will register a sequence of users like this

service_account1@contoso.com
service_account2@contoso.com
service_account3@contoso.com

and so on. If you have only one FE pool in your SfB environment you are now done and may move on.

If you happen to have more than one FE pool in your environment though, you will have to add all of them to the Acano configuration. It is only possible to add 1 through the web interface though, so in this case they will have to be added one by one through the API. You can use Postman or some other REST client for this, or you can use the <a href="http://blog.codesalot.com/2015/12/04/manage-acano-server-with-powershell-psacano-version-0-2-released/" target="_blank">PsAcano </a>powershell module like this:

{ % gist 1422e0d55a80260c1d8f641e191d8542 % }

You can use the same service accounts for all FE pools.

NOTE: The callbridge is added to the SfB environment as a trusted application pool using -TreatAsAuthenticated $true, so we do not need to provide a password for the users as the callbridge is authorized to authenticate users for the SfB environment.
