---
layout: post
title: Communicator phone edition certificates, Standalone CA
date: 2009-10-02 09:43
author: tomlarse
comments: true
categories: [Certificates, Communicator Phone Edition, OCS 2007 R2, Unified Communications]
---
I recently was installing OCS in a domain where we for some reason could not use an enterprise CA, so a standalone was installed. This works fine on the MOC clients, but it was a problem when we were trying to use Communicator Phone Edition.

According to the phone ed. deployment guide, the CPE gets the certificate from AD like this:

<em>1.   The device searches for Active Directory directory objects of category <strong>certificationAuthority</strong>. If the search returns any objects, the device will use the attribute <strong>caCertificate</strong>. This attribute is assumed to hold the certificate and the device will install the certificate.</em>

<em>The Root CA certificate must be published in the <strong>caCertificate</strong> for Communicator Phone Edition. To place the Root CA certificate in the<strong> caCertificate</strong> attribute, use the following command:</em>

<em> certutil -f -dspublish &lt;Root CA certificate in .cer file&gt; RootCA.</em>

<em>2.   If the search for Active Directory objects of category <strong>CertificationAuthority</strong> does not return any objects, or if the objects have empty <strong>caCertificate</strong> attributes, the device searches for Active Directory objects of category <strong>pKIEnrollmentService</strong> in the configuration naming context. Such objects exist if certificate AutoEnrollment was enabled in Active Directory. If the search returns any objects, it will use the <strong>dNSHostName</strong> attribute returned to reference the CA and it will then use the Web interface of the Microsoft Certificates Service to retrieve the Root CA certificate by using the HTTP GET command </em><a href="http://%3cdnshostname%3e/certsrv/certnew.p7b?ReqID=CACert&amp;Renewal=-1&amp;Enc=b64"><em>http://&lt;dNSHostname&gt;/certsrv/certnew.p7b?ReqID=CACert&amp;Renewal=-1&amp;Enc=b64</em></a><em>.</em>

<em>If neither of these methods succeeds, the device displays the error message "Cannot validate server certificate" and the user is unable to use the device.</em>

The certutil command described above requires you to have necessary rights in the forest, which we didn't have.

The solution ended up being:

* Run the server 2k3 reskit tool pkiview.msc
* Right click Enterprise PKI and choose Manage AD Containers
* In the NTAuthCertificates tab, add the root certificate of the standalone CA

That should be it! When we did this the phones started downloading the right certificate.

Edit: This might not be working perfectly. Some phones use an extreme amount of time downloading the right certificate. Might be the messy PKI in the forest being the problem, but i will need to test this some more...
