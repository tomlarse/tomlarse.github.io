title: Tandberg TCAP Day 1
link: http://blog.codesalot.com/2008/08/06/tandberg-tcap-day-1/
author: tomlarse
description: 
post_id: 7
created: 2008/08/06 08:04:00
created_gmt: 2008/08/06 08:04:00
comment_status: open
post_name: tandberg-tcap-day-1
status: publish
post_type: post

# Tandberg TCAP Day 1

Day 1 is going through the basics of Tandberg endpoints.  
  
**LCS/OCS**  
If you want to connect to an LCS server, do not upgrade to F6.3. If you want to connect to OCS, tou must upgrade to F6.3  
  
**External services**  
Through the TMS you have the opportunity to create XML services, much like on the Cisco CallManager. There is an API, but you'll have to make all services yourself. There might be partners that have premade services...  
  
**Number recognition**  
The Tandberg endpoints doesn't have any mechanisms to recognize an H.323 number from an H.320 number, so you will have to define this explicitly under net on the callscreen. It prioritizes H.320 before H.323 when using auto. The same applies to SIP vs H.323 URLs. The H.323 is prioritized. It is possible to mark any setting as default.  
  
**DuoVideo**  
The standard is called H.239, but Tandberg also has a proprietary protocol. H.239 is only used when calling non-Tandberg endpoints. Polycom f.ex. also has their own proprietary protocol, so H.239 will have to be enabled on all endpoints that will be using DuoVideo with other types of endpoints.  
  
**Upgrading**  
When upgrading an endpoint, it may be a good idea to view the progress through the telnet interface to view errors and progress that might not be shown via web or the screen on the endpoint. Also, upgrading via ftp is also possible, but you'll have to use the installation key as username. Password will be the administratorpassword on the endpoint.  
  
Use <http://egil.frontbase.no/> to check if your DNS SRV records are pointing correctly to your gatekeeper!  
  
Great day 1! Learned a lot, and looking forward to the next two days of TCAP.