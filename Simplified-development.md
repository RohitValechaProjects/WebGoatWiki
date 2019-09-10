### With the move towards Java 11 this guide does not work anymore as Spring Boot 1 no longer support DevTools together with Java 11. We need to move to Spring Boot 2 first.


In WebGoat 8 we moved towards Spring Boot in combination with Thymeleaf and AsciiDoc to create a lesson. In the latest commits to develop we refactored the following items:

### Lessons are now loaded with Spring

In WebGoat 6 and 7 we developed our own plugin loader mechanism to load lessons separately into WebGoat. At first we used the same mechanism in WebGoat 8 but with the introduction of Spring Boot we saw a lot of potential to simplify this even more. We now simplified the loading of the lessons and fully rely on Spring capabilities to handle the loading of the plugins, which brings us to the next item

### Speed up development 

From now on we use the [Developer tools](http://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-devtools.html) which enables to keep on developing without restarting the container.
If you use IntelliJ this is completely transparent to you and Spring will redeploy parts of the app as you develop. In IntelliJ create a run configuration for WebGoat:

![Start WebGoat](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/intellij-start.png)

Now let's look at a change we want to make in WebGoat, let's rename the title of the Register page:

![Webpage Registration](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/intellij-1.png)

We open up the `messages.properties` and change the title:

![Webpage Registration](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/intellij-2.png)

Now we recompile the `message.properties` file:

![Webpage Registration](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/intellij-3.png)

And in the Console log we will see Spring restarts the container (only takes a couple of seconds instead of the full startup), and now if we refresh the browser we will see:

![Webpage Registration](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/intellij-4.png)

This is just a simple change but this also works while creating a lesson changing asciidoc files etc etc. This will increase the speed of development. This will definitely bring back the fun in developing a lesson, just compile the 
asciidoc file reload the browser and see your changes.

For Eclipse users the experience should be similar please refer to the Spring documentation mentioned above.


### Simplified creating lessons

In the past we had some difficult conventions to load for example JavaScript files within a lesson. Because Spring 
now handles most of the lesson loading we were also able to simplify the lesson structure itself:

![Structure](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/lesson-structure.png)

Basically everything moved one directory up, which enables us to include JavaScript and css files in a lesson as follows:

```
<link rel="stylesheet" type="text/css" th:href="@{/lesson_css/clientSideFiltering-stage1.css}"/>
<script th:src="@{/lesson_js/clientSideFiltering.js}" language="JavaScript"></script>
````

This is consistent across all lessons, no need to add some strange path in front of the location.





