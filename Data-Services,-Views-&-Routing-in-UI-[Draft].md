Draft ideas/plans for next major release for UI

## Data Services
To share data across the multiple services, the general plan is to have two data services
* Menu
* Lesson
Since these will be provided as services, they can be shared by/injected into multiple views. Speaking of which ...

## Views
One primary view with the following nested views
* menu
* lesson content
* lesson helps
* submission feedback << want to modularize this as opposed to rendering the whole
* heads up-display (e.g. cookies/params or other persistent features)

## Routing
To provide overall better navigation, bookmarking, using browser nav. buttons and to support multiple *.jsp (for certain attacks), we will implement routing. A route will look something like:
`http://server.tld[:PORT#]/webgoat/start.mvc/#lesson/400/117` << This would route to Ajax Security // Same Origin Policy Protection under the current scheme

Optionally, if we want to show/treat _labs_ a little differently, we can also have:
`http://server.tld[:PORT#]/webgoat/start.mvc/#lab/400/125` << This would route to the first lab in Ajax Security.
This could allow for additional checks etc. to be done (pre-requisites) when initiating a lab view as opposed to a lesson view.  We'll need to discuss that yet. And, of course, if we want those to really mean something, said checks need to be double-checked on the server in case of a submission from a lab. We still want to produce respectable app, right?!?

Either way, the routing should allow for us to traverse *.jsp's when needed (although I need to think about that some more still), while primarily staying in the SPA model (and being able to return to it from a separate *.jsp as needed)