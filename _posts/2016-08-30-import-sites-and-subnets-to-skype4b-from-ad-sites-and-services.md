---
layout: post
title: Import sites and subnets to Skype4B from AD sites and services
date: 2016-08-30 07:24
author: tomlarse
comments: true
categories: [Scripts, Unified Communications]
---
Wether it is to use for Call Admission Control or just to get pretty results on the location report on the monitoring server, I usually like to populate network regions, sites and subnets in the Skype for Business topology in every deployment I do.

<img class="alignnone size-full wp-image-947" src="https://codesalot.files.wordpress.com/2016/08/untitled-picture.png" alt="Untitled picture" width="578" height="103" /> Pretty, pretty data :)

In many, if not most, environments I deploy in, the admins have taken their time to set up AD sites and services with the correct site names, so there's no point in doing that job twice. I've made this script which takes the contents of the Sites container and imports it into the Skype for Business topology.

I've come across a couple of ways to convert AD sites to Skype for Business network topology, either adding all sites to one region, or converting the sites to regions themselves and adding offices manually. I also want to expand the script so that you can choose which region and site a given subnet belongs to for each subnet in sites and services.

Usage:

Run the .ps1 and then

```
Import-ADSitesAndSubnets -Regionid Someregion
```

or

``` Import-ADSitesAndSubnets -UseSiteAsRegion ```

And the script:

{% gist 0970a59d99b3ea7be31ca8ca70b838f1 %}

&nbsp;
