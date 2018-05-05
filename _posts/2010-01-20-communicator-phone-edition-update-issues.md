---
layout: post
title: Communicator Phone Edition - Update Issues
date: 2010-01-20 16:32
author: tomlarse
comments: true
categories: [Communicator Phone Edition, CPE, Device Updater, errors, Installation, OCS 2007 R2, problems, Unified Communications]
---
After following several guides to configuring the device update service in OCS 2007 R2, including Rui Silvas <a href="http://blogs.technet.com/ucspotting/archive/2009/03/11/troubleshooting-ocs-2007-r2-device-update-service-for-communicator-phone-edition.aspx" target="_blank">trilogy</a> and Rick Varvels <a href="http://blogs.technet.com/rickva/archive/2009/10/03/ocpe-device-tanjay-upgrade-guide.aspx" target="_blank">guide</a>, I still couldn't get the phones to update the software.

All logs were showing that it had worked, the Update service logs showing that the phone had found the right sw, and IIS logs showing me a 200 OK sent to all phones...

Troubleshooting finally led me to try downloading the CPE.nbt file manually from

<em>http://frontendfqdn/DeviceUpdateFiles_Int/OCInterim/ENU/cpe.nbt</em>

which just gave me a blank page.

I tried comparing the IIS configuration to one I knew was working, and saw that I had a lot less IIS roles installed on the one that was not working.

When I installed this Front End server, i used the commands in <a href="http://www.codesalot.com/2009/installing-ocs-2007-r2-prerequisites-on-windows-server-2008/" target="_blank">this</a> post to install the prereqs. Turns out that if you are going to use CPE, you will probably also need the "Static Content" role service in IIS to configure the correct MIME types on the fileextensions the update serrvice uses.

There exists default MIME types for both the .xml and the .cat extensions that is used by the updater. There is however no default for the .nbt extension.

If this role service is not installed, the updater does not work. You will have to add this feature, and then manually add the correct MIME types to the DeviceUpdateFiles_Int/ and DeviceUpdateFiles_Ext/ folders, which should be:
<blockquote><em>&lt;mimeMap fileExtension=".nbt" mimeType="binary/octet-stream" /&gt;</em>

<em><span style="font-size:x-small;">&lt;mimeMap fileExtension=".cat" mimeType="binary/octet-stream" /&gt;</span></em>

<em><span style="font-size:x-small;">(I have no idea as to why the bottom one is smaller than the other, but I cant get them equal size for some reason :S)</span></em></blockquote>
Hey presto! The phones update themselves like magic has happened!
