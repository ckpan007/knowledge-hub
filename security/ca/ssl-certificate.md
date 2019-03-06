
- [What is SSL](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#what-is-ssl)
 	- [HTTPS in SSL](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#https-in-ssl)
 	- [Website protected by SSL](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#website-protected-by-ssl)
- [SSL can be used to secure](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#ssl-can-be-used-to-secure)
- [What is CA](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#what-is-ca)
   	- [SSL Certificates](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#ssl-certificates)
   	- [Who decides a CA can be trusted](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#who-decides-a-ca-can-be-trusted)
   	- [Different classes of SSL certificates and their use cases](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#different-classes-of-ssl-certificates-and-their-use-cases)
- [What is trust hierarchies](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-or-tls-handshake.md#reference-link)
   	- [Intermdiate CA (ICA)](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#intermdiate-ca-ica)
   	- [Principles using ICA](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#principles-using-ica)
   	- [View root certificates for local computer in Windows](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#view-root-certificates-for-local-computer-in-windows)
   	- [View certificates with Internet Explorer](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#view-certificates-with-internet-explorer)
- [Reference Links](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Knowledge-Warehouse/topiccenter/security/ca/ssl-certificate.md#reference-links)


# What is SSL
Secure Sockets Layer (SSL) was the most widely deployed cryptographic protocol to provide security over internet communications before it was preceded by TLS (Transport Layer Security) in 1999. Despite the deprecation of the SSL protocol and the adoption of TLS in its place, most people still refer to this type of technology as ‘SSL’.

SSL provides a secure channel between two machines or devices operating over the internet or an internal network. One common example is when SSL is used to secure communication between a web browser and a web server. This turns a website's address from HTTP to HTTPS, the ‘S’ standing for ‘secure’.

## HTTPS in SSL
HTTP is insecure and is subject to eavesdropping attacks because the data being transferred from the web browser to the web server or between other endpoints, is transmitted in plaintext. This means attackers can intercept and view sensitive data, such as credit card details and account logins. When data is sent or posted through a browser using HTTPS, SSL ensures that such information is encrypted and secure from interception.

You can look at this video to have an initial understanding about [SSL certificate](https://youtu.be/dsuVPxuU_hc)

## Website protected by SSL
In the case of a browser, you can tell if a site is using SSL when a **padlock** is displayed or the address bar shows the URL as HTTPS instead of HTTP.

Below is a website using SSL:

![ssl website padlock](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Z_ReuseImages/images/ssl/website-padlock.jpg)


# SSL can be used to secure
* Online credit card trasactions or other online payments
* Intranet-based traffic, such as internal networks, file sharing, extranets and database connections.
* Webmail servers like Outlook Web Access, Exchange and Office Communications Server.
* The connection between an email client such as Microsoft Outlook and an email server such as Microsoft Exchange.
* The transfer of files over HTTPS and FTP(s) services, such as website owners updating new pages to their websites or transferring large files.
* System logins to applications and control panels like Parallels, cPanel and others.
* Workflow and virtualization applications like Citrix Delivery Platforms or cloud-based computing platforms.
* Hosting control panel logins and activity like Parallels, cPanel and others.


# What is CA

What are Certificate Authorities & Trust Hierarchies?
Certificate Authorities, or Certificate Authorities / CAs, issue Digital Certificates. Digital Certificates are verifiable small data files that contain identity credentials to help websites, people, and devices represent their authentic online identity (authentic because the CA has verified the identity). CAs play a critical role in how the Internet operates and how transparent, trusted transactions can take place online. CAs issue millions of Digital Certificates each year, and these certificates are used to protect information, encrypt billions of transactions, and enable secure communication.

## SSL Certificates
**An SSL Certificate is a popular type of Digital Certificate that binds the ownership details of a web server (and website) to cryptographic keys**. These keys are used in the **SSL/TLS** protocol to activate a secure session between a browser and the web server hosting the SSL Certificate. In order for a browser to trust an SSL Certificate, and establish an SSL/TLS session without security warnings, the SSL Certificate must contain the **domain name of website** using it, be issued by a trusted CA, and not **have expired**.

According to analyst site Netcraft (www.netcraft.com), in August 2012 there are almost 2.5m SSL Certificates in use for public facing websites. In reality there are probably as many as 50% more than this number in use that cannot be identified by Netcraft on public facing websites. This makes SSL one of the most prevalent security technologies in use today.



## Who decides a CA can be trusted

Browsers, operating systems, and mobile devices operate authorized CA ‘membership' programs where a CA must meet **detailed criteria** to be accepted as a member. Once accepted the CA can issue SSL Certificates that are transparently trusted by browsers, and subsequently, people and devices relying on the certificates. There are a relatively small number of authorized CAs, from private companies to governments, and typically the longer the CA has been operational, the more browsers and devices will trust the certificates the CA issues. For certificates to be transparently trusted, they must have significant **backward compatibility with older browsers and especially older mobile devices** – this is known as ubiquity and is one the most important features a CA can offer its customers.


## Different classes of SSL certificates and their use cases

Prior to issuing a Digital Certificate, the CA will conduct a number of checks into the identity of the applicant. The checks relate to the class and type of certificate being applied for. For example, a domain validated SSL Certificate will have verified the ownership of the domain to be included within the Certificate, whereas an Extended Validation SSL will include additional information on the company, verified by the CA through many company checks.

For the types of certificates and their use cases, please refer to [link](https://www.globalsign.com/en/ssl-information-center/types-of-ssl-certificate/).




# What is trust hierarchies
Browsers and devices trust a CA by accepting the **Root Certificate** into its **root store** – essentially a database of approved CAs that come pre-installed with the browser or device. Windows operates a root store, as does Apple, Mozilla (for its Firefox browser) and typically each mobile carrier also operates its own root store.

## Intermdiate CA (ICA)
CAs use these pre-installed Root Certificates to issue **Intermediate Root Certificates** and end entity Digital Certificates. The CA receives certificate requests, validates the applications, issues the certificates, and publishes the ongoing validity status of issued certificates so anyone relying on the certificate has a good idea that the certificate is still valid.

CAs usually create a number of Intermediate CA (ICA) Root Certificates to be used to issue end entity certificates, such as SSL Certificates. This is called a trust hierarchy, and will look something like this:

![certificates-trust hierarchy](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Z_ReuseImages/images/ssl/globalsign-ev-root.png)

The GlobalSign Extended Validation CA - G2 is shown in this example as the ICA - it’s trust is inherited from the publicly trusted GlobalSign root (top of the hierarchy). This ICA is able to issue publicly trusted end entity certificates, in this example, the ICA issued an Extended Validation Certificate to www.globalsign.com.


### Principles using ICA

CAs should not issue Digital Certificates directly from the root distributed to the carriers, but instead via one or more of their ICAs. This is because a CA should follow best security practices by minimizing the potential exposure of a Root CA to attackers. GlobalSign is one of the few CAs to have always (since 1996) utilized ICAs.


## View root certificates for local computer in Windows
```
a. Open a Command Prompt window
b. Type 'mmc' command and press ENTER key
c. On the File menu, click 'Add/Remove Snap In'
d. Click 'Add'
e. In the Add Standalone Snap-in dialog box, select Certificates
f. Click 'Add'
g. In the Certificates snap-in dialog box, select Computer account and click Next. Optionally, you can select My User account or Service account. If you are not an administrator of the computer, you can manage certificates only for your user account.
h. In the Select Computer dialog box, click Finish
i. In the Add Standalone Snap-in dialog box, click Ok
j. On the Add/Remove Snap-in dialog box, click OK
k. In the Console Root window, click Certificates (Local Computer) to view the certificate stores for the computer
```

After above steps, you shall see all of the certificates installed on your computer.

![view windows root certificates](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Z_ReuseImages/images/ssl/view-windows-certificates.jpg)

## View certificates with Internet Explorer

You can also view, export, import, and delete certificates by using Internet Explorer.

To view certificates with Internet Explorer
```
In Internet Explorer, click Tools, then click Internet Options to display the Internet Options dialog box.

Click the Content tab.

Under Certificates, click Certificates.

To view details of any certificate, select the certificate and click View.
```
![view internet certificates](https://github.wdf.sap.corp/cpcoreChina/c3-coursematerial/blob/dev/Z_ReuseImages/images/ssl/view-internet-explorer-certificates.jpg)





# Reference Links

https://www.globalsign.com/en/ssl-information-center/what-is-ssl/

https://www.globalsign.com/en/ssl-information-center/what-are-certification-authorities-trust-hierarchies/

https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in



