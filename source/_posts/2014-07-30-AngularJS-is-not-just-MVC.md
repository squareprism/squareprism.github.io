---
layout: post
title: AngularJS is not just an MVC framework
categories:
- Articles
tags:
- AngularJS, MVC, Dependency Injection, Extensibility, Testability, Organization, Javascript
status: publish
type: post
published: true 
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

Which Javascript MVC framework should I use? AngularJS or KnockoutJS or Ember or ...? This is a very common question that gets asked by
javascript developers who want to start using MVC in their applications. Most of the answers to such queries
usually conclude with 'it depends' on what you need. But there is a bigger problem, one with the question
itself because Angular (and other frameworks like Ember, Backbone) are not just MVC. They are a lot more.

MVC has been a proven way to address the 'separation of concerns' problem in user interfaces since developers
started using Smalltalk and the pattern got documented in literature on Design and Architecture patterns. As
Javascript development passed the threshold of simple to complex web-apps, MVC found its way into Javascript
in the form  of multiple frameworks. But separation of concerns in the view-model layer is just one of the
problems of Javascript. Unlike other server side languages like Java or C++ that support language level constructs
for organization and dependency management (packages, modules), lifecycle management, extensibility (inheritance and
decoration), and testability via dependency injection, Javascript stays clear of these capabilities. So,
for someone that wants to develop a complex app, these factors become as equally important as the separation of
concerns problem.

**Organization, Dependency and Lifecycle Management**
Angular provides the concept of organizing code using a Module.One can think of a module as a container for the
different parts of your app – controllers, services, filters, directives, etc. Modules  specify how an
application should be bootstrapped. It has a declarative process easy to understand and promotes reuse.To manage
the responsibility of dependency creation, each Angular application has an injector. The injector is a service locator
that is responsible for construction and lookup of dependencies.

**Separation of Concerns**
At the core of Angular are constructs for implementing Template based views, Controllers and data Models. The
framework uses the concept of 'scope' per controller bound to an HTML element in DOM, and takes care of two-way data
binding between the UI and the 'scope'. Developer handle changes to scope within controllers and update their models
appropriately.

**Extensibility**
There are several ways to extend angular and use its features to do work for you. One option is to use specialized
objects called *directives* that help build web components. Another option is to implement *providers". Custom directives
are a powerful feature of Angular and eases code reuse.

**Testability**
Angular provides *Protractor*, an end to end test runner which simulates user interactions that will help one verify
the health of Angular applications. Protractor along with 'DI' based testable code enhances the quality of apps



If all you need is just a simple app implementing MVC (read TodoMVC) that needs to be fast there are many frameworks
that fit the bill and Angular may not be the recommended option. But if you have a large and complex codebase that
requires better organization, testability, extensibility, dependency management, and separation of concerns in the form
of MVC, then a framework such a Angular is the best bet. Above all in Angular as these larger concerns are part of
the framework construct, as our code base grows to large sizes, it allows us maintain our sanity !!
