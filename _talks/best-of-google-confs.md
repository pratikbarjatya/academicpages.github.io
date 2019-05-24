---
title: "Best Google Conferences Collection"
collection: talks
type: "Talk"
permalink: /talks/best-of-google-confs
date: 2019-05-24
location: "Mumbai, India"
---

This is a summary of some of the best Quality Engineering Google Conferences

[Modern Tooling, Testing, and Automation (Chrome Dev Summit 2017) - YouTube](http://bit.ly/2Wvr7bL)
------
Modern web development requires modernizing tooling. In this video, Paul and Eric tour the latest goodies from the Chrome DevTools team.
They cover new features in DevTools, using Lighthouse to guide your development workflow, and automating it all with Puppeteer,
a new Node library for controlling headless Chrome

[Google Test Automation Conference 2015 - YouTube](http://bit.ly/2X2rHe1)
------
GTAC 2015 held at the Google office in Cambridge Massachusetts, on November 10th and 11th, 2015.
- The talks focuses on trends we are seeing in industry combined with compelling talks on tools and infrastructure that can have
a direct impact on Google products.
- This conference is focused for engineers by engineers.
- In GTAC 2015 Google continues to encourage the strong trend toward the emergence of test engineering as a computer science
discipline across companies and academia alike.

[The Clean Code Talks -- Unit Testing](http://bit.ly/2JC6lB6)
------
Google Tech Talks, October, 30 2008
Summary
---
- We can test at different levels
- Unit testing is testing at the class level
- Functional testing is testing at the "group of classes" level (you want to see if a group of classes work together properly)
- Scenario testing is testing at the "application" level (does the application behave correctly as a whole)
- In order to unit test a class, that class must be isolateable (that way, if the test fails, you know exactly who's fault it was)
- In order for a class to be isolateable, all of its dependencies must be passed in its constructor (the class itself must not "new" (create) any instances of the classes it depends on)
- When testing a certain class, you can pass in stub objects, mock objects, or friendly objects to its constructor to satisfy its dependencies
- Whether you pass in stub, mock, or friendly objects, if the test fails, you KNOW its not b/c of the passed in dependencies, therefore it must be the fault of the object being tested
- If you code so that your class gets all of its dependencies in its constructor, then you are doing "dependency injection"

[Testing Engineering@Google & The Release Process for Google's Chrome for iOS](http://bit.ly/2XbtddX)
------
Google NYC Tech Talk Series, August, 19 2014
- Get a peek into iOS development--from making sure our apps and policies stay in compliance with Appstore development restrictions,
 to understanding the interesting points of being a large company that occupies the AppStore alongside individual developers.
- This talk will explore the release process for Chrome for iOS, including an overview of our product development strategy,
 automated testing frameworks, and manual testing processes.

[Is Google always listening: Live Test](http://bit.ly/2QqWC16)
------
Abstract
---
- Does Google and Facebook listen in and record conversations and audio even when they're not open?
- I perform a live test using Google chrome on a Windows 10 PC to discover whether my microphone appears to be recording me
 even when my browser is turned off in order to better target advertisements.
- As pointed out in the comments, there are too many flaws in my methodology to draw any conclusions
 (for instance I am live streaming directly to YouTube which of course necessitates recording my microphone the whole time)

["The Clean Code Talks  -- Inheritance, Polymorphism, & Testing" - YouTube](http://bit.ly/2wjxboV)
------
Google Tech Talks
November 20, 2008
ABSTRACT
---
- Is your code full of if statements? Switch statements? Do you have the same switch statement in various places?
- When you make changes do you find yourself making the same change to the same if/switch in several places? Did you ever forget one?
- This talk will discuss approaches to using Object Oriented techniques to remove many of those conditionals.
- The result is cleaner, tighter, better designed code that's easier to test, understand and maintain.

[Becoming a Software Testing Expert - YouTube](http://bit.ly/2YL6MMU)
------
Google TechTalks
June 13, 2006
# James Bach
ABSTRACT
---
- You're already an experienced tester. You know how to design tests and report bugs.
- Now what? Do you feel like an expert? Unfortunately, if you want to become very good at ...

[Advanced Espresso - Google I/O 2016 - YouTube](http://bit.ly/2Xbu3aB)
------
- Automated UI testing is not an easy matter. With Espresso, a UI testing framework for Android,
 we are helping developers raise the bar for app quality.
- Come to this talk to learn how we're improving Espresso to make handling complex testing scenarios easier.
- We will discuss best practices and examples of advanced Espresso APIs usage for making the most out of your functional tests.
- This session is appropriate for developers already familiar with Espresso as well as those looking to add UI tests to their apps
 for the first time.

[Test-Driven Development on Android with the Android Testing Support Library (Google I/O '17) - YouTube](http://bit.ly/2Wqt60J)
------
- The Android Testing Support Library (ATSL) is the official testing library for Android.
- In this session we give a technical deep dive into ATSL and some of the exciting features that we are adding to make
 it even easier for developers to write high-quality Android apps.
- Stephan Linzner, Nick Korostelev, Jonathan Gerrish and Christian Williams will show you how ATSL can enable test-driven,
 fast iterative development cycles as part of your comprehensive automated testing strategy.
