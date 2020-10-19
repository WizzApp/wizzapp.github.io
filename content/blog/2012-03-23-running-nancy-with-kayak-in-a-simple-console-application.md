---
title: "Running Nancy with Kayak in a simple console application"
date: 2011-03-23
tags: [Nancy, Kayak, software development, CSharp, .NET, console application, self host, OWIN]
RedirectFrom: blog/2012/03/23/running-nancy-with-kayak-in-a-simple-console-application/*
---

Here we go again ...

In the last few days a did some smaller experiments for a new project idea that is spooking around in my head. One of those was to try and get [Nancy](http://nancyfx.org/) up and running with [Kayak](http://kayakhttp.com/) in a simple console application.

[This](http://whereslou.com/2012/01/16/gate-0-2-1-implementation-of-owin-online-at-nuget) post from [Louis DeJardin](http://twitter.com/loudej) provided a good place to start. Most of the post ist still current but there are some changes you have to make to get this up and running. I have no "official" information but I had to change the provided code in the KayakStarter class from this (taken from Louis post):

{% gist 2173428 KayakStarter_old.cs %}

to this:

{% gist 2173428 KayakStarter.cs %}

Did you spot the difference? The only change is the third parameter of the call to the Gate.Hosts.Kayak.KayakGate.Start method. This makes the non-working example files from the NuGet package working again, but it also seems like the Startup class is not used anymore.

Maybe someone with more experience in Kayak/OWIN can shed some light on this?
