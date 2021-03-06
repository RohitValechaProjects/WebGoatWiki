# Frequently Asked Questions

Before contacting webgoat support at webgoat at owasp.org or posting to the [WebGoat mailing list](http://lists.owasp.org/mailman/listinfo/owasp-webgoat), please read the FAQ to see if your question may have been answered.

##### Table of Contents

1. [Q: How do I report a bug?](#bug-report)

1. [Q: How do I get configure WebGoat on different port and/or different IP other then localhost?](#local-host-ip-config)

1. [Q: How do I solve lesson X?](#mailing-list)

1. [Q: How do I contribute to the code i.e. fork/commit?](#forking)

1. [Q: How can I run WebGoat 8 when using Java 11](#java11)


<a name="bug-report"/>

## How do I report a bug?

You can report an issue [here](https://github.com/WebGoat/WebGoat/issues)

<a name="local-host-ip-config"/>

## How do I get configure WebGoat to run on an IP other then localhost?

You can specify the following arguments when starting WebGoat:

```Shell
java -jar webgoat-server-<<version>>.jar --server.port=9090 --server.address=x.x.x.x
```

<a name="mailing-list"/>

## How do I solve lesson X?

Subscribe to the WebGoat mailing list at owasp-webgoat@lists.owasp.org.

Post your question to owasp-webgoat@lists.owasp.org

<a name="forking"/>

##  How do I contribute to the code i.e. fork/commit?

Check out our instructions on [Forking WebGoat in GitHub](https://github.com/WebGoat/WebGoat/wiki/Forking-WebGoat-in-GitHub).

<a name="java11"/>

## How can I run WebGoat 8 when using Java 11 or higher?

The latest releases and develop branch require Java 11, warnings can be suppressed by using the --add-modules parameter:

```
java --add-modules java.xml.bind -jar webgoat-server-8.0.0.VERSION.jar
```