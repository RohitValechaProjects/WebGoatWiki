The WebGoat team is proud to present the first milestone release of version 8. It has
been a long time since the last WebGoat 7 release.

## Quick start

Download the latest jar file [here.](https://github.com/WebGoat/WebGoat/releases/)

Open a console and type:

```$bash
java -jar webgoat-server-<<version>>.jar
```

Open a browser and navigate to: [http://localhost:8080/WebGoat](http://localhost:8080/WebGoat)


## What changed?

### Lessons

The most important change is we moved towards a lesson model instead of 'just hacking' we
now focus on explaining from the beginning what for example a SQL injection is. Each lesson
within WebGoat now contains three elements:

- Explain the vulnerability
- Assignments to learn about how to exploit the vulnerability
- Describe the possible mitigation scenarios

The screenshot shows the start of the lesson. At the top of the page there is a navigation
bar which shows the number of steps within the lesson. A number with a red background means
there is an assignment to solve. When you successfully complete the assignment the background will become green.

![assignment](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/8.0-milestone/assignment.png "Example assignment")
                                                               
As you can see we also thought about the visual appearance of our assignments.

In short: WebGoat is now a **teaching platform** instead of just a hacking platform. 

### WebWolf

We used WebGoat 8 during our workshops/training and we one of the feedback items was that sometimes 
an assignment was not realistic enough: it was difficult to grasp the perspective of the "hacker" vs the user. 
During one of the 'Project summits' at the OWASP AppSec conference we came up with
the idea of creating WebWolf which would make the distinction more clear between actions you are performing as 
a hacker and actions are performed from the perspective of the user.

WebWolf is a completely separate web application which you **can** use to solve assignments. In 
the current version a couple of assignment/challenges use WebWolf. At the moment WebWolf is able
to host files, receive e-mails and serve as a landing page. More details can be found in 
our new WebWolf lesson inside WebWolf.

![WebWolf hosting files](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/8.0-milestone/files.png "WebWolf hosting files")
![WebWolf mailbox](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/8.0-milestone/mailbox.png "WebWolf mailbox")
![WebWolf landing page](https://raw.githubusercontent.com/wiki/WebGoat/WebGoat/images/8.0-milestone/requests.png "WebWolf landing page")

How to get started with WebWolf is described in a lesson within WebGoat, click [here](http://localhost:8080/WebGoat/start.mvc#lesson/WebWolfIntroduction.lesson)

**Big thanks to OWASP for making it possible for us to go to the Project summits at AppSec conferences**

 
### Challenges/CTF

During a couple of conferences we were asked to host a small Capture the Flag event with WebGoat. The first one 
 was a success so we added a separate section in WebGoat with CTF challenges. Some of the challenges have a direct 
 connection with the lessons but a couple of them are more for fun. Having the CTF challenges has two purposes:
 
* As a teacher you can start WebGoat to host only the challenges (next release)
* A lesson can point to a specific challenges to solve in which a user of WebGoat can test the knowledge of a vulnerability (end challenge)
