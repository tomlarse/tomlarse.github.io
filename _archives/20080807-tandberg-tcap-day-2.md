title: Tandberg TCAP Day 2
link: http://blog.codesalot.com/2008/08/07/tandberg-tcap-day-2/
author: tomlarse
description: 
post_id: 8
created: 2008/08/07 07:14:00
created_gmt: 2008/08/07 07:14:00
comment_status: open
post_name: tandberg-tcap-day-2
status: publish
post_type: post

# Tandberg TCAP Day 2

**Tandberg MPS is the topic of the day**  
  
The MPS is a gateway and a MCU in the same box. Comes in two versions, MPS 200 and 800. The 200 is a 3U box with 2 module spaces. The 800 is a 9U box with 8 module spaces.  
  
It supports transcoding, which is translation between different codecs. If one system uses H.264 with G.722 and the other uses H.263+ G.722, the MPS will translate this.  
  
It will also do ratematching, so in a multiconference, users can connect with different speeds. One can be 384kbps, one can be 512kbps and another one can be 768kbps. One conference can only use 2 different speedgroups, so if one user connects with 384kbps, and the next connects with 768kbps, a user that connects with 512kbps will get 384kbps back. He will send with 512kbps though. The two groups of speeds will always be the highest and the lowest of the speeds connected. This means that if you have one group with 768kbps and one with 512kbps, if a user connects with 384kbps, the user with 512kbps will be downgraded to 384kbps.  
There is also a third group, but this is reserved for cellular systems.  
  
Use chart on slide 37 for MPS capacity and scaling information.  
  
**Installation**  
Even though the MPS is 10/100 capable and has autosensing, it is smart to force switch and MPS media cards to 100 full duplex. This is due to different implementations of the autosensing feature from different switchmanufacturers. With normal computers, this is normally not noticed, because you seldomly use realtime traffic, but with videoconferencing, more or less all traffic is realtime and because of this duplex mismatch problems are more severe.  
  
**Use**  
When creating a conference where the MPS/MCU will call out to a TCS-4 system, put the main number in the number field, and the extension in the SubAddress field.  
  
It is important to create a good numberplan before implementation begins. You need several prefixes for functions as conferences and outgoing connections, and they cannot crash with each other.  
  
In the gateway settings, do not set the "percent of total bandwith" to zero. This will obviously render the gateway useless.  
  
**Troubleshooting**  
  
The MPS has two modes on commandline. In addition to the commandline that exists on all Tandberg systems, it has also got a UNIX subsystem that contains files and folders, where the eventlog will be as txtfiles. To enter the UNIX system, use 'root' as a username in stead of 'administrator'.  
  
In an environment where there are a lot of different systems, when users experience problems with the conferencing system, check Fast Update Requests, FUR. The MPS will not handle them very well.  
  
**We managed to get in a bit of TMS at the end of the day as well**  
  
To manage Tandberg classic endpoints, you need to run version B4 and later.  
  
  
  
Fun fact: On an endpoint, press the phonebook key 10 times, and you will get a menu filled with games :D