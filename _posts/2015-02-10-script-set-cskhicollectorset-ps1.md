---
layout: post
title: Script: Set-CsKhiCollectorSet.ps1
date: 2015-02-10 14:59
author: tomlarse
comments: true
categories: [CQM, KHI, Lync 2013, script, Scripts, Unified Communications]
---
Lync Key Health Indicators are an essential tool in health monitoring your Lync deployment, and is the first step in deploying the Lync <a href="http://blogs.technet.com/b/jenstr/archive/2013/10/23/call-quality-methodology-cqm.aspx" target="_blank">Call Quality Methodology </a>

After adding the KHI counters to applicable Lync servers, it can be quite the chore to log in to all of them to start the performance counters. It is possible to reach all computers from a Performance Monitor snapin, but with a lot of servers that too can take some time.

This script finds all servers that normally run KHI counters, and starts or stops the counters on them. It can also get the current running status of the counters. It is also possible to supply a csv with servers to run on to the script.

Download latest version <a href="https://github.com/tomlarse/Set-CsKhiCollectorSet/releases/latest" target="_blank">here</a>
