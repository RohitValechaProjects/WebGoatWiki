## Overview

The WebGoat project is hosted at [github/WebGoat](https://github.com/WebGoat-Legacy). 

Contributions are welcome! A large portion of Webgoat lessons are community contributed.

This page describes the WebGoat development process.

## Roles

* **Core developers**. have **access to the WebGoat repository**, as well as the ability to **create**, **assign**, and **resolve** JIRA tickets
* **External contributors**. have limited access to JIRA, but can **contribute** by forking the Webgoat repo.
* **WebGoat admins**. have admin **access to the WebGoat Bamboo**, **JIRA** and **github** repos to **approve new users**

Webgoat admins promote external contributors to core developers whenever it makes sense. If you'd like to join the team, we'd love to hear from you! [Contact Bruce Mayhew](mailto:webgoat@owasp.org) for more information.

## Repository Setup and Release Process

Master is the main working stream. [This bamboo job](https://webgoat.atlassian.net/builds/browse/WEB-WGM) builds it nightly, producing a numbered version for each build.  This is the bleeding edge version, the 'nightly build'. 

You can find [the latest nightly build](https://webgoat.atlassian.net/builds/browse/WEB-WGM/latest), and [a list of all recently nightly builds](https://webgoat.atlassian.net/builds/browse/WEB-WGM) in bamboo.

If you have access, [you can view the WebGoat builds](https://webgoat.atlassian.net/builds/browse/WEB)

WebGoat build numbers have a three-part structure:  <major>.<minor>.<buildNumber>.   For example, 6.1.65. 

Anything you merge to master needs to be at least good enough to go into the nightly build. That means:

1.          all of the tests pass
1.          nothing is _worse_ than it was before you started

Releases are also cut from the master branch, using a separate, administrator-executed bamboo job. This job tags master, and produces a stable, longterm release.  Stable releases are available for download on the [main WebGoat Page](http://webgoat.github.io)

## Development Workflow for Contributors 

Contributors do not have direct repository access, but that doesn't mean contributions are not welcome!  

If you'd like to help out, just fork the Webgoat Repository and make a pull request. Contributers should follow these steps:

1. **Create a gihub account**, if not already existing.
1. **Fork the Webgoat repository** at [https://github.com/WebGoat/WebGoat-Legacy](https://github.com/WebGoat/WebGoat-Legacy).
1. **Create a topic branch** for the changes. If you are working on a Webgoat JIRA issue, use the ticket number as the topic branch name. If there is no JIRA ticket, use a sensible name.
1. **Develop and test your changes**  to make sure your changes are ok.
1. **Create a Pull Request**. When you are ready to contribute your code. This is done via the github website. Please rebase your commits on top of master, so that your changes are easy to pull. If you don't know how to do that, [here's is a good overview](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request).
1. **Core developer merges changes** If your changes look good, a core developer will merge the change into master.  Your changes will be available in the nightly build. If the changes needed more work, that is coordinated on the pull request thread. 

If you are not an experienced git user, these tutorials might help:

* [Setting up Git](https://help.github.com/articles/set-up-git)
* [Forking a repo](https://help.github.com/articles/fork-a-repo)
* [About Pull Requests](https://help.github.com/articles/using-pull-requests)

## Development Workflow for Core Developers

The workflow for core developers is very similar to that of contributors. The main differences are that creating a fork is not necessary, and JIRA references are mandatory. 

Core developers, of course, may also merge pull requests from external contributors. In which case. the flow starts at step 6.

Core Developers should follows these steps when working on issues:

1. **Create a topic branch** for the changes. Use the ticket number as the topic branch name. If there is no JIRA ticket, you should get/make one.
1. **Develop and test your changes** to make sure your changes are ok.
1. **Push your changes to origin** This makes your branch available for others to review.
1. **[Optional] Get Feedback, if needed** If you need someone else to test, they can check out your branch. If the change is simple, you might just move directly to the pull request.
1. **Create a Pull Request**. This is done via the github website.  When you think your changes are ready, make a pull request for the merge into master.  Though you could easily merge directly, this ensures another developer knows about the change, and has reviewed it.  
1. **A different Core developer merges changes** Your changes will be available in the nightly build. If the changes needed more work, that is coordinated on the pull request thread. It is preferred to merge pull requests through the github website, unless there are conflicts.  Not only is it easier, but it is less prone to error.

    * If a pull request cannot be merged on the website, it is ok to ask the originator to rebase their pull request on master.  This is more work for the requestor. However, it is almost always the right thing to do because it will have the original author resolving merge problems, not the reviewer.  If this seems unfamiliar, [this might help](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request).

## A word about the dark side....

Though it is tempting, when developing for WebGoat, you should not work off of your local master branch. There are two reasons why this is a bad idea:

1.       You wont be able to easily work on multiple things without stashing
1.       When your pull request is merged into the target branch, the person merging your pull request may decide to rebase your commits to avoid a merge commit, or to squash the commits into a single coherent commit. If your pull request was from your 'master' branch, you will encounter problems when merging the target branch back into your own 'master'. 