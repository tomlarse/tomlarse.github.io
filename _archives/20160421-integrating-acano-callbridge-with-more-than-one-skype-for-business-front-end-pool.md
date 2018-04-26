title: Integrating Acano callbridge with more than one Skype for Business Front End pool
link: http://blog.codesalot.com/2016/04/21/integrating-acano-callbridge-with-more-than-one-skype-for-business-front-end-pool/
author: tomlarse
description: 
post_id: 833
created: 2016/04/21 16:47:39
created_gmt: 2016/04/21 16:47:39
comment_status: open
post_name: integrating-acano-callbridge-with-more-than-one-skype-for-business-front-end-pool
status: publish
post_type: post

# Integrating Acano callbridge with more than one Skype for Business Front End pool

When integrating an Acano callbridge with Skype for Business (or any of the Lync versions), one of the tasks needed is to provide the callbridge with one or more SfB-enabled users that it can use to obtain MRAS credentials so that it can send media through the SfB edge server to external SfB users. This user is also used by the callbridge to look up SfB conference ID's when using multi-homed conferencing.