---
title: "Brainstorming: Automatic updates for Winforms/WPF applications"
date: 2011-11-24
tags: [brainstorming, software development, CSharp, .NET, windows forms, WPF, automatic updates]
RedirectFrom: blog/2011/11/24/brainstorming-automatic-updates-for-winforms-slash-wpf-applications/*
---

_This post is the first of a collection of [brainstorming](/blog/categories/brainstorming/) articles I'll write in the near future. These are primarily meant to note down my thoughts on specific projects and/or feature implementations etc._

Currently a lot of ideas whirl around in my head (which have nothing to do with my potential future project, of course ;-). One of those is an automatic update feature for windows client applications.

The idea is that there are two main components:

* An update server which is a web service of some kind. This server would include some tooling to allow for easier package creation (more on that later).
* A client library which you can use to enable automatic updates. This may include dialogs for user notification.

### The client

The application using the client would include a public key. The packages provided by the update server would be simple zip archives containing an xml file with relevant data (name of the application, version etc.) and the updated component (either an msi file or a dll for simple plugins). The xml file also contains a SHA1 hash of the updated component and will be signed with the private key corresponding to the public key stored in the application.

On startup or whenever the client application would check the update server for updates like this:
{% gist 1391207 ClientApplication.cs %}

The client can also send additional data (like license keys etc.) as an optional parameter in the GetVersionInfo method which may then be processed by the update server. This would change the webervice call above to something like this:
{% gist 1391207 ClientApplication2.cs %}

If the user chooses to download the update, the client application will download the whole zip file, extract it and first verify the signature of the xml file against the embedded public key and then the SHA1 hash against the downloaded update to verify its integrity. This should avoid most of the security risks as long as the update server is called via https and has a valid certificate.

The developer of the application will be able to choose whether a valid ssl certificate will be enforced on the client or not.

### The server

As mentioned above the server stores update packages and provides a webservice to retrieve the current available version of an application and the update itself.

The server should store those updates in a single directory (maybe one subfolder for each application or updatable component). In the first step the server would only support the creation of the update package via a command line tool (e.g. a Powershell script):
{% gist 1391207 CreatePackage.ps1 %}

This will ask the user for the passphrase for the private key and generate the xml file with the hash and signature automatically. It will also copy the output (both the update component and the xml file) to the directory provided in the --out parameter.

The zip file for download will be created and cached on demand by the server. Later on a push of updates via the webservice itself may be implemented.

When the client asks for the version info the server will return the values from the xml in the applicable application subfolder. This means the client is responsible for checking if the provided version is newer or not.

Handling of additional data provided by the GetVersionInfo call can be easily added to the service by adding a custom version handler to an internal dictionary:
{% gist 1391207 Webservice.cs %}

This is what I have in mind so far, I guess there will be a follow up post to this when more thoughts come up ;-)
