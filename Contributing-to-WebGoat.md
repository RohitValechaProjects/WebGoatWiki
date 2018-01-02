## Overview

The WebGoat project is hosted at [github/WebGoat](https://github.com/WebGoat). 

Contributions are welcome! A large portion of Webgoat lessons are community contributed.

This page describes the WebGoat development process.

## Roles

* **Core developers:** have **access to the WebGoat repositories** and can merge pull requests
* **Contributors:** can **contribute** by forking and submitting pull requests.


If you'd like to join the team, we'd love to hear from you! [Contact Bruce Mayhew](mailto:webgoat@owasp.org) for more information.  

_If you just want to fix an issue that's been nagging you, we welcome that too._

## Repository Setup and Release Process

The ```develop``` is the main working stream. We use _Travis.CI_ as a _"Continuous Integration"_ server for testing each pull request and after merge into develop.

You can view the status of our build processes and jobs on [Travis.CI](https://travis-ci.org/WebGoat/WebGoat)

WebGoat build numbers have a three-part structure:  <major>.<minor>.<buildNumber>.   For example, 7.0.65. 

Anything you submit as pull request to be merged into develop is expected to be at least good enough to go into the the bleeding edge build. That means:

1.          all of the tests pass
2.          nothing is _worse_ than it was before you started

Releases are cut from the master branch, by a process triggered by a _core developer_. This job tags master, and produces a stable, longterm release.  Stable releases are available for download on the [main WebGoat Page](http://webgoat.github.io)

## Development Workflow for Contributors 

Contributors do not have direct repository access, but that doesn't mean contributions are not welcome!  

If you'd like to help out, just fork the [WebGoat Repository](https://github.com/WebGoat/WebGoat) on GitHub, make your changes and submit a pull request. 

Here is a breakdown of the steps for contribution:

1. **Create a GitHub account**, if not already existing.
1. **Fork the WebGoat repository** at [https://github.com/WebGoat/WebGoat](https://github.com/WebGoat/WebGoat).
1. **Create a local git branch** for your changes. If you are working on a WebGoat issue, use the GitHub Issue number/id as the topic branch name. If there is no Github Issue, use a sensible name. We recommend the creation of a Git Branch for your changes because the development pace on the main branch is very fluid, which means you can easily become out of synch with the upstream (WebGoat/WebGoat) develop branch. Using a Git Branch for your changes will allow you to rebase your work on top of the ```develop``` branch whenever necessary.
1. **Develop and test your changes**  to make sure your changes are ok.
1. **Create a Pull Request**, when you are ready to contribute your code. This is done via the GitHub website. Please rebase your commits on top of develop, so that your changes are easy to pull. If you don't know how to do that, [here's is a good overview](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request).
1. **Core developer merges changes** If your changes look good, a core developer will merge the change into develop.  Your changes will be available in the _bleeding edge build_ . If the changes needed more work, that is coordinated on the pull request thread. 

If you are not an experienced git user, these tutorials might help:

* [Setting up Git](https://help.github.com/articles/set-up-git)
* [Forking a repo](https://help.github.com/articles/fork-a-repo)
* [Collaborating / Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
* [About Pull Requests](https://help.github.com/articles/using-pull-requests)

## Development Workflow for Core Developers

The workflow for core developers is very similar to that of contributors. The main differences are that creating a fork is not necessary, and Github issue references are mandatory. 

Core developers, of course, may also merge pull requests from external contributors. In which case. the flow starts at step 6.

Core Developers should follows these steps when working on issues:

1. **Create a topic branch** for the changes. Use the ticket number as the topic branch name. If there is no JIRA ticket, you should get/make one.
1. **Develop and test your changes** to make sure your changes are ok.
1. **Push your changes to origin** This makes your branch available for others to review.
1. **[Optional] Get Feedback, if needed** If you need someone else to test, they can check out your branch. If the change is simple, you might just move directly to the pull request.
1. **Create a Pull Request**. This is done via the github website.  When you think your changes are ready, make a pull request for the merge into develop.  Though you could easily merge directly, this ensures another developer knows about the change, and has reviewed it.  
1. **A different Core developer merges changes** Your changes will be available in the __Bleeding Edge build__. If the changes need more work, that is coordinated on the pull request thread. It is preferred to merge pull requests through the GitHub website, unless there are conflicts.  Not only is it easier, but it is less prone to error.

    * If a pull request cannot be merged on the website, it is ok to ask the originator to rebase their pull request on develop.  This is more work for the requestor. However, it is almost always the right thing to do because it will have the original author resolving merge problems, not the reviewer.  If this seems unfamiliar, [this might help](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request).

## A word about the dark side....

Though it is tempting, when developing for WebGoat, you should not work off of your local develop branch. There are two reasons why this is a bad idea:

1.       You wont be able to easily work on multiple things without stashing
1.       When your pull request is merged into the target branch, the person merging your pull request may decide to rebase your commits to avoid a merge commit, or to squash the commits into a single coherent commit. If your pull request was from your 'develop' branch, you will encounter problems when merging the target branch back into your own 'develop'. 