## Use Docker (only for version 7.1 and higher)

The easiest way to start WebGoat is to use Docker. 

1. Run it Docker:

```
docker run -p 8080:8080 webgoat/webgoat-7.1
```

2. Browse to [http://localhost:8080/WebGoat](http://localhost:8080/WebGoat) and happy hacking !


## Standalone

1. Download the easy run executable jar file which contains all the lessons and a embedded Tomcat server [here](https://github.com/WebGoat/WebGoat/releases/download/7.1/webgoat-container-7.1-exec.jar)

2. Run it using java:

Open a command shell/window, browse to where you downloaded the easy run jar and type:

```Shell
java -jar webgoat-container-7.1-exec.jar
```

3. Browse to [http://localhost:8080/WebGoat](http://localhost:8080/WebGoat) and happy hacking !

## Run WebGoat on a different port

By default WebGoat will run on port 8080, if you need it to run on a different port you can use: 

```Shell
java -jar .\webgoat-container-7.1-exec.jar -httpPort=8081
```





