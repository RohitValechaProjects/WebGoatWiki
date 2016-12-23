## Use Docker (only for version 7.1 and higher)

The easiest way to start WebGoat is to use Docker. 

1. Run it Docker:

```
docker run -p 8080:8080 webgoat/webgoat-7.1
```

2. Browse to [http://localhost:8080/WebGoat](http://localhost:8080/WebGoat) and happy hacking !


## Standalone

1. Download the easy run executable jar file which contains all the lessons and a embedded Tomcat server:

https://github.com/WebGoat/WebGoat/releases/

2. Run it using java:

Open a command shell/window, browse to where you downloaded the easy run jar and type:

```Shell
java -jar webgoat-container-<<version>>-war-exec.jar
```

3. Browse to [http://localhost:8080/WebGoat](http://localhost:8080/WebGoat) and happy hacking !

## Run WebGoat on a different port

By default WebGoat will run on port 8080, if you need it to run on a different port you can use: 

```Shell
java -jar .\webgoat-container-<<version>>-war-exec.jar -httpPort=8081
```

## Using proxy tools

Some of the lessons need a proxy to intercept request towards the WebGoat server.

### Using OWASP Zed Attack Proxy (ZAP)

By default the local proxy in ZAP listens on port 8080. You have two options, change the settings in ZAP or change the default port of WebGoat. In ZAP go to Options --> Local proxy --> change port (8084)

* Start ZAP 
* Run WebGoat
* Configure the browser

In your browser lookup the network settings and set the proxy address to `localhost:8084`.

In order to see if the proxy is able to intercept the requests, enable the break on all request/responses: Tools --> Toggle break on All request.
Now go to http://localhost:8080/WebGoat and check in ZAP whether the request has been intercepted.

### Using Burp Suite 

By default the local proxy in Burp listens on port 8888 (see Proxy --> Options)

* Start Burp Suite
* Run WebGoat
* Configure the browser.

In your browser lookup the network settings and set the proxy address to `localhost:8084`.

In order to see if the proxy is able to intercept the requests, enable interception of all request (Proxy --> Intercept --> Press Intercept is on)
Now go to http://localhost:8080/WebGoat and check in Burp whether the request has been intercepted.





