title: #Lync mobility failing after #CU5
link: http://blog.codesalot.com/2012/06/15/lync-mobility-failing-after-cu5/
author: tomlarse
description: 
post_id: 394
created: 2012/06/15 12:53:24
created_gmt: 2012/06/15 12:53:24
comment_status: open
post_name: lync-mobility-failing-after-cu5
status: publish
post_type: post

# #Lync mobility failing after #CU5

If mobility is failing after applying CU5 and your symptoms are a 500 internal server error when browsing https://fepool.contoso.com/mcx/mcxservice.svc, try the steps in this blogpost. Seems to be an issue with the web.config file in the mcx folders in IIS after the update. I've had this happen with both int and ext web.config.