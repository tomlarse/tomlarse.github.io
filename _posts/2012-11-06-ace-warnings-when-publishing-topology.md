---
layout: post
title: ACE warnings when publishing topology
date: 2012-11-06 08:59
author: tomlarse
comments: true
categories: [errors, Forest prep, Lync, Lync 2010, Lync Server 2010, Publish topology, quickfix, Topology Builder, Unified Communications, warnings]
---
Now and then when publishing the topology, I've gotten some warnings that just states one or more of these:

<strong>Warning:</strong> Ace DOMAIN\RTCUniversalGlobalReadOnlyGroup; Allow; ReadProperty; None; None

and also later in the log

<strong>Warning:</strong> One or more group access control entries (ACEs) are not ready.

This means that not all ACEs are ready after the forest prep, for whatever reason. Just run a

```
Enable-CsAdForest
```

which should reset the permissions, and you should be fine.

<a href="http://technet.microsoft.com/en-us/library/gg425713(v=ocs.15).aspx">http://technet.microsoft.com/en-us/library/gg425713(v=ocs.15).aspx</a>
