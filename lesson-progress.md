## Lesson progress

### Introduction

The "Congratulations" message was changed due to the following [bug](https://github.com/WebGoat/WebGoat/issues/169). Basically it means the progress is only mentioned as a green check mark in the lesson menu.

The source of this issue is the fact that the image from the message in the lesson gets loaded after the loading of the complete lesson content. See the following image:

![Message flow](https://github.com/WebGoat/WebGoat/blob/master/webgoat-container/src/documentation/csrf-lessons.png)

In the "Message gets displayed" step the lesson is not yet marked as completed because this will happen when the image gets loaded (last step). In the "message gets displayed" step the message snippet:

```
<div id="message" class="info"><%=webSession.getMessage()%></div>
```
does not mark the lesson as complete because the loading of the image (last step) will invoke the method `makeSuccess`. Due to this order the message will not be shown on the screen.

The only visual indicator for a user is the menu showing a green check mark.

### Solution

Based on the reloading of the menu (after the lesson content gets displayed) we have added a new JavaScript model and view which can track the lesson progress. This gives us the ability to display the "Congratulations" message also for the CSRF lessons.

#### New endpoint

The backend provides a new endpoint called `lessonProgress` which returns the following JSON message:

```json
{
  "lessonCompleted" : true|false,
  "successMessage" : "Congratulations..."
}
```
The success message is included in the message to provide the user interface with the language specific "Congratulations" text.

#### JavaScript

On the JavaScript side we have added a new model called `LessonProgressModel` and `LessonProgressView` both contain a straightforward implementation. The `LessonController` will call the function `lessonCompleted` the same way the menu gets reloaded which will in turn render the view.

#### Future

The use of the lesson progress controller can be used more in the future. It now only contains the "Congratulations" message but it can also provide progress during the labs.


