---
title: "Why use Continuous Integration?"
date: 2012-06-29
tags: [software development, tools, practices, continuous integration, development workflow, automatic build]
RedirectFrom: blog/2012/08/01/why-use-continuous-integration/*
---

### TL;DR;

[Continuous Integration](http://en.wikipedia.org/wiki/Continuous_integration) means that all changes are continuously integrated into a common integration branch. This allows for faster "compatibility" checks between various development branches, faster failure in case of test errors resulting from those changes and therefore less time developers have to spend hunting for issues that keep them from developing.

### Continuous integration and development workflow

From a developer point-of-view, continuous integration means that you should integrate the changes in your local development branch into a central integration branch as soon as possible. Note the wording "integration branch". Changes committed to this integration branch may not necessarily be released as there may be still work to be done before the corresponding feature/bugfix is done. This leads to the following branches in your SCM:

* master (from which the releases are built)
*     development/integration (as the name says ;-)
*     a number of feature branches

and the following development workflow:

1.          The developer works on a feature branch.
2.          As soon as he wants to commit his changes to the integration branch (which should happen at least once a day, possibly 	more often), he merges his changes from this feature branch into the integration branch.
3.          After that he checks that his changes do not break anything on his local machine (project still compiles, tests still pass) and then
4.          pushes his changes to the central repository.

From there, an automated build server gets the lastest version and does a clean build. This ensures that the developer merged everything needed to build the project (sometimes a source file does not get committed etc.), which in turn ensures that each developer can continue working as expected then he gets the lastest sources.

### Ensuring the integrity of the build

The workflow above should ensure that the automated build always passes. When this is not the case, fixing the build is the highest priority for the development team, as a broken build means that either

*     A feature is broken (marked by a failing test ... hopefully)
*     A test is broken (either because of changed requirements or brittle tests)
*     The project does not compile (which hinders other developers from getting the latest source and integrating their changes)

### Tools

Continuous integration can be done totally by hand. You do not need a build server to check the build, you can do the clean build yourself. Nevertheless there are several tools (or classes of tools) that help you during the workflow:

*     A build server like [TeamCity](http://www.jetbrains.com/teamcity/), [Bamboo](http://www.atlassian.com/software/bamboo/overview) etc.
*     A DCVS like [Mercurial](http://mercurial.selenic.com/), [Git](http://git-scm.com/) or [Bazaar](http://bazaar.canonical.com/en/)

As I said, you can do Continuous Integration without those or with other tools, but especially a DCVS eases the integration process.

### Complementary practices

Practices like TDD (and its various cousins) and automatic testing in general in combination with a build server allow you to verify the integrity of your project regularly. You can of course leave those out of the chain, but if you do automatic builds you should absolutely integrate automated tests as well (and everyone knows you should do TDD in any case, right ;-).
