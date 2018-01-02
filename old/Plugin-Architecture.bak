# Plugin modification Scenarios

Plugins should be easy to modify.  There are two scenarios where this may occur:

1. **As a part of a LAB lesson**, the user needs to modify the source code.  Ideally, plugins allow this modification to occur without a restart, and using only a text editor, so that it is easy to complete lessons.  Ability to edit files on the the filesystem is a great bridge to later functionality to allow editing them directly in the IDE.

2. **As a part of learning** and/or starting your own lesson, it should be as easy as copy-paste to start with an existing lesson and make a new one.  

With luck, learning and fiddling will lead a user to spend the time to make a new lesson, which leads to the next section

# Plugin Authoring Scenarios

We want it to be easy to extend WebGoat.  Webgoat is extended using lessons, which teach a particular security topic.  There are two main scenarios in which a a user might add a lesson:

1. **In-house**.  In this case, the lessons are used for internal training, and are not intended to be contributed to the community. In this case:
    * The lesson source is separate from the WebGoat source
    * The user would probably prefer to use a binary distribution of Webgoat, so that they can periodically upgrade it very easily. IE, java -jar WebGoatBinary-exec-war.jar
    * When the user upgrades webgoat, they want their lessons to appear, but not to be overwritten
    * The user does not want to bother with a git clone
    * the user really doesnt want to deal with a Java IDE

2. **Contributors**. In this case, the user authors lessons with the intent of contributing them back to the community. In this case:
    * The user is best served by starting with a git clone, because they eventually need to submit a pull request
    * The user runs WebGoat from source with mvn tomcat:run-war
    * It is highly desirable for the user to be able to re-load lessons without restarting tomcat. Otherwise its just a huge pain to develop
    * A Java IDE is probably more likely here, but again it shouldnt require a restart to make changes.

# Plugin format

Each plugin contributes a lesson. Each lesson contributes:

* A controller, which does logic and processing. This controller is authored in a script language, such as Groovy, so that it is short and reload-able
* A dynamic view, which the user sees when working with the lesson
* static resources, which include images, styles, etc

A plugin is simply a folder that follows a standard format. I based this format off the grails layout with tweaks to add stuff specific to webgoat and remove stuff we don't use:
```
/lesson_{unique_lesson_id}
  config.json
  /controllers
  /assets
   (js and css go here)
  /views
  /i18n
    messages.properties
    messages_es.properties
    ...
  /lesson_plans
    (english at root, localized plans under locale folders)
    /fr
    ...
  /lesson_solutions
    (english at root, localized solutions under locale folders)
    /fr
    ...
  /hints
```

* Note that hints and views will use the message bundles under i18n for localization
* Lesson plans and solutions will probably be easier to author in the native language and drop in the locale folder rather than using the message bundles but I am open to change on this point 
* config.json holds lesson configuration (name, menu entries, custom configuration entries)
* controllers can be either MVC controllers or REST based on annotations (will leverage springmvc)
* I am thinking of using groovy for controllers as it's close enough to Java for the java folks but doesn't require the compile/deploy cycle and syntax is easier for the people who prefer scripting
* Not sure exactly of the view. Will either be jsp, gsp, thymeleaf or freemarker (how's that for narrowing it down!)

There are two ways to distribute lessons:

1. by storing the folder structure in WebGoat source tree. These are called **core-plugins**
2. by creating this folder structure and creating a .zip file. It can be deployed into a running Webgoat by expanding it in the plugins folder.

# How it works

On startup, Webgoat ( even the self-run war file ) will expand its lessons into a 'plugins' directory on the file system, and set up tasks that watch for changes to the controllers and views. 

A user can modify them as necessary without a restart. The most common use case would be a user completing the LABS.

If a user would like to deploy new lessons, new folders can be created in the 'plugins' directory.  The most common example would be to copy an existing lesson. The core distribution should include one or two examples that are suitable for copying as a starting point for a new lesson.


A system property 'WebGoat-Plugins-dir' allows the user to specify where the 'plugins' directory is. If found, Webgoat will use that folder for lessons.  On startup, it will expand core lessons into that folder (overwriting those that are there). That way, a user who has lots of local lessons can just upgrade the WebGoat jar, and running WG will update built-in lessons automatically.



