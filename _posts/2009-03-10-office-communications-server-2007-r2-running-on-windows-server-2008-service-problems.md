title: Office Communications Server 2007 R2 running on Windows Server 2008 service problems
link: http://blog.codesalot.com/2009/03/10/office-communications-server-2007-r2-running-on-windows-server-2008-service-problems/
author: tomlarse
description: 
post_id: 18
created: 2009/03/10 10:11:00
created_gmt: 2009/03/10 10:11:00
comment_status: open
post_name: office-communications-server-2007-r2-running-on-windows-server-2008-service-problems
status: publish
post_type: post

# Office Communications Server 2007 R2 running on Windows Server 2008 service problems

I have on a couple of occations now experienced problems with the services on OCS 2007 R2, when running on 2008 server. I seems that the services hang during boot, and this causes all other services to halt startup as well.  
  
The first time i experienced this, the server seemed to hang on "Configuring updates" during boot, though this was not the case.  
  
The solution has been to either set all OCS services to "Automatic (delayed startup)", or to keep the front end service to "Automatic" and all other OCS services to delayed.  
  
I dont know why this happens, and I haven't been able to figure it out. If someone has an idea of why, please let me know.