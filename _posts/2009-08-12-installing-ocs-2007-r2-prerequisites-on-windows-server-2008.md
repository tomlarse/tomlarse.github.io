---
layout: post
title: Installing OCS 2007 R2 Prerequisites on Windows Server 2008
date: 2009-08-12 13:09
author: tomlarse
comments: true
categories: [Installation, OCS, OCS 2007 R2, prerequisites, Unified Communications, Windows Server 2008]
---
This post was not written by me, but by my excellent colleague <a href="http://msunified.net/2009/08/12/installing-ocs-2007-r2-prerequisites-on-windows-server-2008/" target="_blank">Ståle</a>. Kudos! Pay his blog a visit ^^

TI

---

Commands to install the necessary prerequisites for OCS 2007 R2 on Windows Server 2008

<strong>Front End on Windows Server 2008
</strong><em>Servermanagercmd.exe -install web-windows-auth web-mgmt-compat web-mgmt-console web-http-logging msmq-server msmq-directory powershell was-process-model was-config-apis rsat-addc</em>

Installs the following components:
<ul>
	<li>[Web-Windows-Auth] – Windows Authentication</li>
	<li>[Web-Mgmt-Compat] – IIS 6 Management Compatibility</li>
	<li>[MSMQ-Server] – Message Queuing Server</li>
	<li>[MSMQ-Directory] – Directory Service Integration</li>
	<li>[RSAT-ADDC] – Active Directory Domain Controller Tools</li>
	<li>[WAS-Process-Model] – Process Model</li>
	<li>[WAS-Config-APIs] – Configuration APIs</li>
	<li>[Web-Mgmt-Console] – IIS Management Console</li>
	<li>[Web-Http-Logging] – HTTP Logging</li>
	<li>[PowerShell] – Windows PowerShell</li>
</ul>
The last 3 in the list are not required, but they are highly recommended. IIS 7.0 Management Console is IMHO much easier to use than the IIS 6.0 version. The logging tools often come in handy when troubleshooting OCS IIS issues and PowerShell makes working with OCS WMI values a piece of cake.

<strong>Monitoring Server on Windows Server 2008</strong>
<em>Servermanagercmd.exe -install msmq-server msmq-directory</em>

Installs the following components:
<ul>
	<li>[MSMQ-Server] – Message Queuing Server</li>
	<li>[MSMQ-Directory] – Directory Service Integration</li>
</ul>
<strong>CWA Server on Windows Server 2008</strong>
<em>Servermanagercmd.exe -install web-windows-auth web-mgmt-compat web-mgmt-console web-http-logging </em>

Installs the following components:
<ul>
	<li>[Web-Windows-Auth] – Windows Authentication</li>
	<li>[Web-Mgmt-Compat] – IIS 6 Management Compatibility</li>
	<li>[Web-Mgmt-Console] – IIS Management Console</li>
	<li>[Web-Http-Logging] – HTTP Logging</li>
</ul>
<strong>Mediation Server on Windows Server 2008</strong>
<em>Servermanagercmd.exe -install rsat-addc</em>

Installs the following components:
<ul>
	<li>[RSAT-ADDC] – Active Directory Domain Controller Tools</li>
</ul>
Post used as a reference for this post

<a href="http://waveformation.com/2009/06/02/installing-ocs-2007-r2-prerequisites-on-windows-server-2008/">http://waveformation.com/2009/06/02/installing-ocs-2007-r2-prerequisites-on-windows-server-2008/</a>
