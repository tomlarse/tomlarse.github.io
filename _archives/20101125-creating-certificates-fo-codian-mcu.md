title: Creating certificates for Codian MCUs
link: http://blog.codesalot.com/2010/11/25/creating-certificates-fo-codian-mcu/
author: tomlarse
description: 
post_id: 151
created: 2010/11/25 10:27:34
created_gmt: 2010/11/25 08:27:34
comment_status: open
post_name: creating-certificates-fo-codian-mcu
status: publish
post_type: post

# Creating certificates for Codian MCUs

If you want to use HTTPS (without the annoying browser certificate warnings) or MTLS with a Codian MCU, you'll need to install a certificate on the MCU.

## Comments

**[Egil Hasting](#30 "2011-01-29 23:25:13"):** Great post! Keep on updating the blog with more video stuff :)

**[Timo](#31 "2012-02-09 10:03:21"):** openssl x509 -in .cer -inform DER -out .pem -outform PEM

