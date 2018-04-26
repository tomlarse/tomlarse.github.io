title: Tandberg TCEP Day 1
link: http://blog.codesalot.com/2008/08/11/tandberg-tcep-day-1/
author: tomlarse
description: 
post_id: 10
created: 2008/08/11 07:20:00
created_gmt: 2008/08/11 07:20:00
comment_status: open
post_name: tandberg-tcep-day-1
status: publish
post_type: post

# Tandberg TCEP Day 1

Todays topic is Call Control Components - GK, VCS-C, VCS-E  
  
  
  
When you factory reset these units, all option keys will disappear.  
  
  
  
  
  
When a CCC is in routed mode, RAS. Q931 and H.245 info will go through the device, as opposed to non-routed mode, where only RAS will pass through the device. In SIP, all calls are in routed mode, but with H.232 this is optional. The VCS is always in routed mode though.  
  
  
  
The VCS has a SIPH.232 interworking feature. Note that using this interworking feature will count as 1 traversal call.  
  
For the sake of redundancy, there is a possibility to set up alternate Gatekeepers. When using this, the endpoint will recieve a list of alternate gatekeepers. If the gatekeeper the endpoint is registered to goes down, the endpoint will connect to the next endpoint on the list. Be sure to set the H.323 TTL down to something shorter than 1800 seconds if the environment demands faster recovery from an outage. Note that a gatekeeper can only be alternate to another gatekeeper, and a bordercontroller can only be alternate to another bordercontroller, a gatekeeper can not be alternate to another bordercontroller and the other way around. This also applies to VCScontrol/express.