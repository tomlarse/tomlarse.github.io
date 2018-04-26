title: Audiocodes MP-1xx Initial IP configuration
link: http://blog.codesalot.com/2008/07/10/audiocodes-mp-1xx-initial-ip-configuration/
author: tomlarse
description: 
post_id: 6
created: 2008/07/10 14:09:00
created_gmt: 2008/07/10 14:09:00
comment_status: open
post_name: audiocodes-mp-1xx-initial-ip-configuration
status: publish
post_type: post

# Audiocodes MP-1xx Initial IP configuration

I recently experienced difficulties with the initial ip configuration on an MP-118 FXO.  
  
After I had configured the IP address on the quick install page, the only available button to push is "reset", no "save", "apply" or "submit" buttons are available. In my simple mind this meant that I had to push reset. Did not turn out to be a good idea. I could not make contact with the mediagateway on the new IP or the old. I tried keeping the "reset" button on the back pressed for more than 6 seconds, hoping it would get factory settings, thinking I had messed up the IP-address when I punched it in. But it made no difference. Noticed in that in the manual it said I could set the IP via bootp, so I downloaded a dhcpserver that supported bootp, and like magic I could contact the mediagateway again.  
  
I tried setting the IP again, but the same thing happened when i moved the gateway to its final position in the rack. I then set the IP once more with bootp, and looked through the configuration settings. I discovered the "burn to flash" feature, and thought I had found my mistake. But no. Same thing again.  
  
After yet another round of bootp IP setting, I found the IP settings under the "Advanced Configuration" tab, and this page had a "submit" button. And lo-and-behold! this time it worked.  
  
Probably a bug in the firmware that the IP won't stick when you configure it at the "Quick configuration" page, but at least now I know about it.  
  
Other than that, the Audiocodes gateway seems ideal for OCS voip implementation in SMB's!  
  
PS: I wrote this purely on my recollection of it, so the button names and configuration page names may not be accurate!