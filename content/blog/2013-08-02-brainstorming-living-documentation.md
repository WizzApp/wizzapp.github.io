---
title: "Brainstorming: Living documentation"
date: 2013-08-02
tags: [brainstorming, software development, living documentation, software architecture, practices, specifcation by example]
RedirectFrom: blog/2013/08/15/brainstorming-living-documentation/*
---

_So it's been awhile since my last [brainstorming](/blog/categories/brainstorming/) article (almost 2 years), but here is another one ;-)_

{% img right http://www.daniel-rosendorf.de/images/library.jpg %}

### Introduction

So, I'm reading again ... after what seems like years I decided to read something "technical" again and this time I want to tackle [Specification By Example](http://specificationbyexample.com/) by [Gojko Adzic](http://gojko.net/). After not even finishing the fist chapter an idea that I had some months ago came back to me.

### The premise

Imagine a typical software project with detailed specifications and a lot of automated acceptance tests (both of which do exist in every project, right? ;-). In "Specification By Example" Gojko talks about _living documentation_, which means that specifications are _executable_ and are _validated frequently_ against the project.

Basically the specifications and the examples included are acceptance tests that get executed during the build and reflect the current development progress.

### The problem

Unless you are using something like the [Gherkin]() language to do your specifications, there will be no really easy way to translate specifications into tests and test cases that some system can automatically execute. So now what?

### The solution (as invented by me ;-)

You already have automatic tests in place and you already have the build fail if a test fails which in turn means you already have a test report. Everything that's missing is a system to capture the specifications and some way to map the captured specifications to one or more automatic tests.

So that's what we are going to build.

### The web application

The web application has a basic user management and allows for the following things:

* Capture specifications (either directly in the web interface or through some kind of import, MS Excel would come to mind ... although I really do not know why :P)
* Show current state of implementations (Not implemented, Ok, Failing)
* Map specifications to tests in a test result report
* Upload test result reports

### The setup

For this to work the projects test results need to be uploaded to the web application. This can either be done manually (HINT: Don't!) or automatically by your CI server. For this the web application provides a simple API endpoint to post the documents to.

### The workflow

Let's assume we have a specification that we need to implement. We already have it in the system, so when a customer logs into the web interface the specification is shown as "Not implemented". Now the developer has implemented some or all examples/test cases and the current test results got automatically uploaded to the application. So the developer logs in, selects the not yet implemented specification and is then able to map test results to this specification, so that after the mapping is done and the developer checks a checkbox during mapping that says "These are all test cases, there will not be any more" the specification and/or its examples will be shown as "Ok". The mapping is stored so that when a mapped test fails, the project overview will be updated and show the status as "Failing".

From here on, advanced workflows can be started, e.g. if a specification fails is it because requirements have changed or because of technical dependencies in the system (which probably should not be there).

### Great, what now?

I honestly don't know ... but I will make this some kind of conceptual series and blog about design details. So maybe at the end, we have a complete specification that we can implement ;-)

---

Image courtesy of [Yuri Levchenko](http://www.flickr.com/people/i8ipod/).
