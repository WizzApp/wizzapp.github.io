---
title: "Lowering the entry barrier for new developers on an existing project"
date: 2012-05-18
tags: [software development, practices, tools, nuget, roundhouse, continuous integration, continuous delivery, project management]
RedirectFrom: blog/2012/05/23/lowering-the-entry-barrier-for-new-developers/*
---

### What is this all about?

This post is a short compilation of suggested practices to ease the entry barrier for developers coming into an already running project. As I'm mainly using the .NET Framework and Visual Studio I will describe options that refer to this setup.

This is purely a thought experiment at the moment: None of the things mentioned here were actually implemented or used by me, although I guess there are projects out there (commercial and open source) that use things from this list and I will certainly take care that future projects that I'm involved in will include some of the things mentioned below.

### Things you should have/do

1.  _Have an easy way to set up a local development database._ Use either a tool like [RoundhousE](https://github.com/chucknorris/roundhouse "RoundhousE") or something like [EF Migrations](http://blogs.msdn.com/b/adonet/archive/2012/02/09/ef-4-3-automatic-migrations-walkthrough.aspx "Entity Framework 4.3 Automatic migrations walkthrough").
2.  _Have documentation that points to places (or people) of interest (e.g. source control, build server, extended documentation)._ Suggestions here would be a ReadMe document in the solution folder etc.
3.  _If additional software has to be installed to open projects in Visual Studio, provide a simple script that installs them if necessary_. Examples would be ASP.NET MVC projects etc.
4.  _Have all necessary libraries in a folder within the source control so that they are checked out with the project_ (or have a script/tool that installs them like the [restore option of NuGet](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages "Using NuGet without committing packages"))

The very simple goal for this is that a developer checks out a project and immediately has all the things necessary to start working on it without having to contact or disturb another dev.

Note that environment specific assumptions in scripts and tools may exist (e.g. the users machine has to be connected to a specific VPN to successfully execute the script etc.) but this means that they have to be taken care of first.
Also take care to provide good error messages and advice if something in the scripts goes wrong.

### Why go through all the trouble?

There are several reasons to do all this:

1.  If you are a small software shop, chances are that you need to shift developers frequently. Making it easy for developers to actually develop is just naturally a good thing to do.
2.  Some of the practices above have the additional benefit that they integrate and help with automated builds and [Continuous Integration](http://martinfowler.com/articles/continuousIntegration.html "Continuous Integration") (and its more advanced form of [Continuous Delivery](http://en.wikipedia.org/wiki/Continuous_Delivery "Continuous Delivery"))

## Final thoughts

Practices shown in this article are overlooked most of the time. But I do not think that they take too much time to setup ... at least if you include them from the very beginning in your project. However as mentioned above I do not have the real world practice I'd like to have in this topic which in turn means that I will be missing a lot of points. If anyone has something to add to this list, feel free to leave a comment. I'll try to update this post now and then to keep this list as current as possible.
