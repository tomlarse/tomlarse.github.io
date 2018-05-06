---
layout: post
title: Creating certificates for Codian MCUs
date: 2010-11-25 10:27
author: tomlarse
comments: true
categories: [Certificates, Cisco Telepresence, Codian MCU, video conferencing]
---
If you want to use HTTPS (without the annoying browser certificate warnings) or MTLS with a Codian MCU, you'll need to install a certificate on the MCU.

Remember that you'll need the "Encryption" release key to enable SSL in any form. This is a free key that kan be ordered from TAC.

Under Network -&gt; SSL certificates, you'll find this screen:

<a href="http://codesalot.files.wordpress.com/2010/11/cert1.jpg"></a>

<a href="http://codesalot.files.wordpress.com/2010/11/cert.jpg"><img class="alignnone size-medium wp-image-156" title="certificat_config" src="http://www.codesalot.com/wp-content/uploads/2010/11/cert-300x124.jpg" alt="Certificate config" width="300" height="124" /></a>

So we need to provide a certificate and a private key corresponding to the certificate, which means that we need to create a CSR and import both the key and the certificate to the MCU.

I'll show how to do this using openSSL and a Windows CA. If there is an OCS/Lync implementation in the environment, you could use the wizard to create the cert, but you would have to split it up with something like openSSL afterwords anyway, so the easiest thing is just to create it all with openSSL.

openSSL can be found for almost any platform, I use <a href="http://www.slproweb.com/products/Win32OpenSSL.html" target="_blank">openSSL for win32</a> 
<h3>Create the CSR</h3>
Use this command to create the CSR
´´´openssl req -new -newkey rsa:2048 -nodes -out <strong>&lt;name_of_the_cert&gt;</strong>.csr -keyout <strong>&lt;name_of_the_key_file&gt;</strong>.key -
subj "/C=<strong>&lt;countrycode&gt;</strong>/ST=<strong>&lt;state&gt;</strong>/L=<strong>&lt;City&gt;</strong>/O=<strong>&lt;Organisation&gt;</strong>/OU=<strong>&lt;Organisational Unit&gt;</strong>/CN=<strong>&lt;fqdn.of.mcu&gt;</strong>"´´´
Exchange all the <strong>&lt;variables&gt;</strong> with the correct values.

This should create two files, <strong>&lt;name_of_the_cert&gt;</strong>.csr and <strong>&lt;name_of_the_key_file&gt;</strong>.key and place them in the same directory as you run the command.
<h3>Create the cert</h3>
Copy the .csr file to the CA. In a cmd window, navigate to the folder you copied the .csr to and run:
´´´certreq -submit -attrib "CertificateTemplate: WebServer" <strong>&lt;name_of_the_cert&gt;</strong>.csr´´´
If the CA is configured to issue certs automagiacally, you should have be asked where to save the .cer. If not, you'll have to open the CA MMC snapin and issue the cert manually.
<h3>Add the cert to the MCU</h3>
Back on the MCU, browse to the .cer in the Certificate field and the .key in the Private Key field. Leave the password field empty. Restart the MCU and you should be good to go.
<h3>Creating a trust store</h3>
The trust store to be uploaded needs to be in .pem format. Export the root certificate you need to trust to a DER encoded file. (normally .cer) and run the following command:
´´´openssl x509 -inform der -in <strong>&lt;rootcert&gt;</strong>.cer -out <strong>&lt;rootcert&gt;</strong>.pem´´´
<strong>&lt;rootcert&gt;</strong>.pem can be uploaded as the trust store. <a name="PemToDer"></a>
