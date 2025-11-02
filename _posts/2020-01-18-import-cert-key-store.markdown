---
layout: post
title:  "Import a Signed Certificate Into a New Key Store"
date:   2020-01-18 15:04:19 -0500
categories: apache development software tomcat java 
---
Are you a software developer? Do you need to setup Tomcat with a secure connector using an existing signed certificate? If you follow the directions laid out in the post then you should be up and running quickly.

## What you'll need:

* GNU/Linux Host
* Apache Tomcat Installation
* Root Access
* A Signed Certificate
* The Private Key File for the Signed Certificate

### Create PKCS12 File

First create a PKCS12 file using the signed certificate and key.

{% highlight bash %}
root@www0:~# openssl pkcs12 -export -in runbymany.com.crt -inkey runbymany.com.key -name *.runbymany.com -out runbymany.com.p12
{% endhighlight %}

### Create KeyStore File

Second, you will need to create a keystore using the signed certificate and key.

NOTE: Select a value for PASSWORD and remember it.

{% highlight bash %}
root@www0:~# keytool -importKeyStore -deststorepass PASSWORD -destkeystore runbymany.com.jks -srckeystore runbymany.com.p12 -srcstoretype PKCS12
{% endhighlight %}

### Update Server.xml and Restart Tomcat

Finally, you will need to update your server.xml with the new configuration (remember to substitute PASSWORD with what you used previously and to change PATH_TO_TOMCAT to the installation directory of Apache Tomcat):

{% highlight xml %}
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
maxThreads="1000" scheme="https" secure="true"
SSLEnabled="true" keystoreFile="PATH_TO_TOMCAT/conf/runbymany.com.jks"
keystorePass="PASSWORD" clientAuth="false" sslProtocol="TLS" maxPostSize="97589953"
URIEncoding="UTF-8" tcpNoDelay="true" enableLookups="false" disableUploadTimeout="true"
acceptCount="100" minSpareThreads="20" emptySessionPath="true" maxHttpHeaderSize="8192"/>
{% endhighlight %}


If you’ve questions about any of this I encourage you to use the contact form on my website [here][here].

Cheers! and Happy Hacking!

-Adam

[here]: https://www.runbymany.com/contact
