![WebGoat Logo](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/wg_logo_snag.png)

# What is WebGoat?
 
WebGoat is a deliberately insecure application that allows interested developers
just like you to *test vulnerabilities* commonly found in Java-based
applications that use common and popular open source components.

Now, while we in no way condone causing intentional harm to any animal, goat or
otherwise, we think learning everything you can about security vulnerabilities
is essential to understanding just what happens when even a small bit of
*unintended code gets into your applications*.

What better way to do that than with your very own scapegoat?

Feel free to do what you will with Hack. Poke, prod and if it makes you feel
better, scare him until your heart’s content. *Go ahead, and Hack the goat*. We
promise he likes it.

Thanks for your interest! 

_The WebGoat Team_

# Runtime environment for OWASP WebGoat

The following picture shows the ideal local setup for running WebGoat and following the lessons. It also shows WebWolf and how OWASP Zap can be used between the browser and OWASP WebGoat. 

![WebGoat local configuration](https://zubcevicdotcom.files.wordpress.com/2020/02/owasp-setup.png?w=1024)

# Releases

WebGoat consists of two applications that work together. One is called WebGoat and one is called WebWolf.
WebWolf depends on WebGoat and requires that WebGoat is started first. 

Both WebGoat and WebWolf are runnable jar files. Make sure the following ports are available: 80, 8080, 9090, 9001 when running locally.

There are several options to run WebGoat (and WebWolf):
+ Fork/Clone the repository, checkout the develop branch, build the artifacts using Java 11 and Maven 3.6+, and run the archives.
    ``` 	
    mvn clean install
    java -jar webgoat-server/target/webgoat-server-v8.0.0-SNAPSHOT.jar
    #then in another shell
    java -jar webwolf/target/webwolf-v8.0.0-SNAPSHOT.jar
    ``` 
+ Download the released and build jar files and run using Java 11
    + [Standalone WebGoat 8.0](https://github.com/WebGoat/WebGoat/releases/)
+ Use the all-in-one docker container which contains a reverse proxy and both WebGoat and WebWolf which start in the correct order
    + [Docker WebGoat 8.0](https://hub.docker.com/r/webgoat/goatandwolf/)
    ```
    docker run -d -p 80:8888 -p 8080:8080 -p 9090:9090 -e TZ=Europe/Amsterdam webgoat/goatandwolf:latest
    ``` 

# Older releases
* [Docker WebGoat 7.1](https://hub.docker.com/r/webgoat/webgoat-7.1/)
* [Standalone WebGoat 7.1](https://github.com/WebGoat/WebGoat/releases/)
* [WebGoat 7.0.1](https://github.com/WebGoat/WebGoat/releases/tag/7.0.1)
* [WebGoat Legacy releases](https://github.com/WebGoat/WebGoat-Legacy/releases)
