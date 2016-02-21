---
author: abualsamid
comments: true
date: 2014-12-13 22:31:22+00:00
layout: post
slug: estratex-2014r7-release
title: eStratEx 2014R7 release.
wordpress_id: 17
categories:
- StratEx
---

The 2014R7 release of our flagship software has been released last night. As our users know, we release in place, with no down time and no interruptions. There has been nearly 50 items in this release, those impacting the end user are detailed in the release notes. We will have a separate blog post describing some of the functional changes in this release but I wanted to touch on some of the technical changes today.

As you may know the eStratEx stack is built on a MySQL back-end running on Ubuntu. We use Percona MySQL and not just because Percona is a client, as we used them before they became a client, but because of its superior performance.

The data access layer and the business layer are written in .NET, specifically VB.NET and C#. They currently run on II7 deployed on Windows 2008R2 but with the recent decisions of Microsoft to open up .NET and to make it truly cross platform we may be running it on Ubuntu in the future.

The front end is written using HTML, Javascript, CSS. We hand crafted a lot of our front end code with jQuery being the main library we typically used in our system. As of this release we are starting to use Bootstrap V3 for eStratEx.

[![eStratEx Login](images/eStratEx-Login-300x142.png)](images/eStratEx-Login.png)

This will allow us to provide a crisp, modern, refresh to our user interface. It will also allow us to focus on Mobile First strategy, where each aspect of our application is meant to run beautifully in your favorite mobile device. After some debate we chose this approach over releasing a handicapped, limited app providing minimal functionality to our users as have been adopted by others.

In conjunction with our [Bootstrap v3](http://getbootstrap.com/) change we have switched to using [Knockout v3](http://knockoutjs.com/). We have used knockout in the past on few admin pages but now we are fully embracing the Model-View-View Model (MVVM) pattern across the application. Our front end and middle layers are now very similar to what Microsoft is doing with their [Azure](http://azure.microsoft.com/) portal.  When we started eStratEx however ASP.NET MVC was a very nascent technology and thus we went with class asp.net web forms. Two million lines of code later we are not about to re-do our system in MVC. However, all the neat stuff Microsoft is doing for web forms is making that a moot point. We are using Friendly URLs, as [described](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) by Microsoft's Scott Hanselman ([@shanselman](https://twitter.com/shanselman)), and URL routing to build out MVC style interface using web forms. Microsoft has a vision for a unified ASP.NET and we are capitalizing on that fully.

As soon as you login to the application you will start to notice the new changes made possible via combining the best of knockout, bootstrap, .Net and MySQL.



cross posted on stratex.com/blog
