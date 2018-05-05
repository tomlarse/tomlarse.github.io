---
layout: post
title: #Lync mobility failing after #CU5
date: 2012-06-15 12:53
author: tomlarse
comments: true
categories: [500 internal server error, bugs, CumulativeUpdates, Lync, Mobility, Unified Communications]
---
If mobility is failing after applying CU5 and your symptoms are a 500 internal server error when browsing https://fepool.contoso.com/mcx/mcxservice.svc, try the steps in this blogpost. Seems to be an issue with the web.config file in the mcx folders in IIS after the update. I've had this happen with both int and ext web.config.

<a href="http://brekkjen.wordpress.com/2012/04/15/lync-mobility-failing-after-cu5">http://brekkjen.wordpress.com/2012/04/15/lync-mobility-failing-after-cu5</a>
