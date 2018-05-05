---
layout: post
title: Automating FIM Run Profiles for Lync
date: 2015-04-09 22:18
author: tomlarse
comments: true
categories: [Central Forest, FIM, Forefront Identity Manager, Lync, Multiple Forests, Unified Communications]
---
When deploying Lync in a Central Forest Topology it is recommended to use a directory synchronization product of some sort to synchronize user accounts from user forests to the central resource forest as contact objects. Nowadays this is normally handled by Forefront Identity Manager, and this deployment is discussed in detail in the Technet <a href="https://technet.microsoft.com/en-us/library/gg670889(v=ocs.14).aspx" target="_blank">white paper.
</a>

When FIM is deployed, you have to execute Run Profiles on the management agents in the correct order, both import and metaverse synchronization needs to be done on the central forest management agent before any user forest management agents for the data to be exported correctly in the last step. This means that in general the Run Profiles needs to be run in this order: (This applies to both Full and Delta executions)
<ul>
	<li>Import  Central Forest Management Agent</li>
	<li>Import User Forest 1 Management Agent</li>
	<li>Import User Forest 2 Management Agent</li>
	<li>Sync Central Forest Management Agent</li>
	<li>Sync User Forest 1 Management Agent</li>
	<li>Sync User Forest 2 Management Agent</li>
	<li>Export Central Forest Management Agent</li>
</ul>
Also it is a good idea to wait until the last operation is completed before starting the next.

This gets quite tedious rather quickly when you have to right-click the management agent -&gt; run, select the correct profile, then click OK for every operation. In addition you will need to think about automation at some point as well.

So I've created this powershell function that will take a sorted array of Management Agent names and run all the Run Profiles in the correct order for you.

Simply load the functions in your current powershell session and run

[sourcecode language="powershell"]
CsFimMaRun -ManagementAgents @(&quot;ResourceForest&quot;,&quot;UserForest1&quot;,&quot;UserForest2&quot;) -Type Full
[/sourcecode]

or

[sourcecode language="powershell"]
CsFimMaRun -ManagementAgents @(&quot;ResourceForest&quot;,&quot;UserForest1&quot;,&quot;UserForest2&quot;) -Type Delta
[/sourcecode]

and the run profiles should be executed in order. For automation just add one of the above to the end of the script and run that in a windows task scheduler. One delta update a day is often enough, but if the environment is very dynamic you might want to run it more often.

If you set $debugpreference="Continue" it'll display the status after each operation as well.

Download <a href="https://github.com/tomlarse/CsFimRunProfileExecution/releases/latest">here</a>
