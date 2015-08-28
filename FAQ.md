# Frequently Asked Questions

Before contacting webgoat support at webgoat at owasp.org or posting to the [http://lists.owasp.org/mailman/listinfo/owasp-webgoat WebGoat mailing list], please read the FAQ to see if your question may have been answered.

##### Table of Contents

1. [Q: How do I report a bug?](#bug-report)

1. [Q: I put the WebGoat war file in my tomcat/webapps directory and the http://localhost/WebGoat/attack URL doesn't work.?](#tomcat-directory)

1. [Q: I dropped the WebGoat war file into my non-Tomcat application server, why doesn't WebGoat seem to work?](#non-tom-cat-app-server)

1. [Q: I'm having problems with the maven build working properly. How do I configure my environment so that I don't receive errors?](#and-file)

1. [Q: Why does WebGoat stop functioning right after startup?](#startup)

1. [Q: How do I get configure WebGoat to run on an IP other then localhost?](#local-host-ip-config)

1. [Q: How do I solve lesson X?](#mailing-list)

1. [Q: How do I contribute to the code i.e. fork/commit?](#forking)

<a name="bug-report"/>
##  How do I report a bug?

Today we are tracking defects with [http://webgoat.atlassian.net Jira]. You will need to register before you can file a ticket.  We hope to resolve that soon or move to the github issue tracking system. 

***

<a name="tomcat-directory"/>
## I put the WebGoat war file in my tomcat/webapps directory and the http://localhost/WebGoat/attack URL doesn't work.

Rename the downloaded war file to WebGoat.war.  Delete the existing tomcat/webapps/*WebGoat* directories. Restart Tomcat.

You can also create an tomcat embedded server build.  Look in the [https://github.com/WebGoat/WebGoat-Legacy/wiki/Installation-(WebGoat-6.0) Installation Wiki]
***

<a name="non-tom-cat-app-server"/>
## I dropped the WebGoat war file into my non-Tomcat application server and WebGoat doesn't seem to work.

Make sure you are going to http://localhost:8080/WebGoat.  You should see a login page

***

<a name="ant-file"/>
## I'm having problems with the maven build working properly. How do I configure my environment so that I don't receive errors:

Look in the [https://github.com/WebGoat/WebGoat-Legacy/wiki/Installation-(WebGoat-6.0) Installation Wiki]
***

<a name="startup"/>
## When I start up WebGoat it dies very quickly.

WebGoat is a Java application that runs on Tomcat using port 80.  If you have another application listening on port 80 (like IIS), you will need to change WebGoat's port (to 8080 or something) in the tomcat_root/conf/server.xml file.  You can also start up webgoat using the webgoat_8080.bat file.  You will then need to browse to:

```
    http://localhost:8080/WebGoat/attack
```


***

<a name="local-host-ip-config"/>
## How do I get configure WebGoat to run on an IP other then localhost?

In the webgoat.bat file, in the root directory, the following lines are executed: 

```
      delete .\tomcat\conf\server.xml 
      copy .\tomcat\conf\server_80.xml .\tomcat\conf\server.xml 
```

This will overwrite any changes you may have made to server.xml file that addressed this issue.... 

By changing the server_80.xml file (or by removing the above code from webgoat.bat, after making your changes) you can reflect your changes to the Tomcat configuration. You will need to change the IP address in the server_80.xml file to be the IP of the host machine.

The following connectors should be modified

```
      <!-- Define a non-SSL HTTP/1.1 Connector on port 8080 --> 
      <Connector address="10.20.20.123" port="80" 
      ... 
      <!-- Define a SSL HTTP/1.1 Connector on port 8443 --> 
      <Connector address="10.20.20.123" port="443" 
      .... 
```

where the 127.0.0.1 will be replaced by your IP. In this case 10.20.20.123

***

<a name="mailing-list"/>
## How do I solve lesson X?

Subscribe to the WebGoat mailing list at owasp-webgoat@lists.owasp.org.

Post your question to owasp-webgoat@lists.owasp.org

<a name="forking"/>
##  How do I contribute to the code i.e. fork/commit?

Check out our instructions on [Forking WebGoat in GitHub](https://github.com/WebGoat/WebGoat-Legacy/wiki/Forking-WebGoat-in-GitHub).