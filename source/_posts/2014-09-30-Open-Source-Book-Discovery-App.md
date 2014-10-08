---
layout: post
title: Open Source Book Discovery App - LocalReads
categories:
- Articles
tags:
- Books, Book Discovery, Local, Search, Grails, Ionic, Angular, TDD, BDD, Jasmine, Protractor, Karma, Websockets, MongoDB
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

I worked on an idea for discovery of books a couple of years ago. The idea was simple - make a catalog of your paper books
online and tag your location to it. Friends and neighbours would then be able to search for a book using the service and
discover books in your shelf. The service would allow making requests for books and manage subsequent interactions between
users. I tried developing this concept in residential communities, colleges and online book groups but did not get significant
traction to pursue it as a serious business.

In the couple of years that followed there were many others who approached or discussed the same idea online and otherwise.
I discouraged some of the folks explaining my experiences with traction. I am sure many more would want to try it out. But
the fact that there are many people with the same idea points to a possible passionate market however small it maybe. Most of
the code I had developed was lying idle and I thought it would help folks trying to build this concept from scratch if I
open sourced the codebase.

In the last few weeks I refactored the old code and built out a [mobile app](https://play.google.com/store/apps/details?id=com.squareprism.localreads.ver1) with the same backend, but used newer technologies
to build better capabilities and with less code. I have published the app for free on Android platform. You can check it out
at [here](https://play.google.com/store/apps/details?id=com.squareprism.localreads.ver1). The code is open source and published in github.

![localreads](/images/localreads-android-page.png)

The android app is developed using the [Ionic-Angular framework](http://www.ionicframework.com) that lets you build hybrid
(html + native) apps. The backend service is implemented as a set of REST apis using [Grails](http://www.grails.org) with
a MongoDB database. You can check out the code on github at the following locations.

- LocalReads Mobile App Codebase - [https://github.com/sathishc/localreads](https://github.com/sathishc/localreads)
- LocalReads backend service - [https://github.com/sathishc/localreads-service](https://github.com/sathishc/localreads-service)


See instructions for building the codebase in the corresponding github repositories. The front end code uses Protractor/Jasmine for
End-to-End testing and Karma/Jasmine for unit tests. The backend uses Spock framework for testing the apis. 

The code base will help developers trying to build similar capabilities for other apps - location
based full-text search, real-time messaging, restful and stateless service, hybrid mobile app using cordova, etc

To build a full stateless restful service in grails I have used the [Spring Security Rest plugin](https://github.com/alvarosanchez/grails-spring-security-rest)
as the normal spring security based authentication relies on sessions to be maintained. Real-time messaging is 
implemented using [Spring Websockets](http://grails.org/plugin/spring-websocket). Reach out if you are looking for help in these areas.

All of the code is distributed under the Creative Commons License 4.0.

