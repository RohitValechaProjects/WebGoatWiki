## Using proxy tools

**Please note: ** WebGoat 8.0 contains a lesson on how to configure OWASP ZAP.
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

