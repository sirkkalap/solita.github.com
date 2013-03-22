---
layout: post
title: Simple functional testing with browser
author: petrisi
excerpt: Testing functionality of a web application can be automated using Selenium and WebDriver. This is a very basic tutorial to start doing that. In this article I cover some design decisions that support this approach.
tags: testing selenium webdriver java solita tutorial
---

### About this article ###

In this article my goal is to get started with functional testing through a web interface. Secondarily I try to refine the code so that it is easier to maintain and read.

This article will not cover how to run functional test automatically on a continous integration platform. Nor will this article and the code example cache the browser instance so that multiple tests could use it efficiently.

Another issue that is not covered here is how to manage test fixture and test data robustly and efficiently.

Yet another issue that is skipped here is how to cope with dynamic documents, ajax requests, javascript events that fire when the page is ready etc. These make efficient and robust testing a bit more challenging.

So, this in mind, lets start with a look at the test setup.

### Basic test setup ###

I choose to use our www.solita.fi as the web application for testing. The page contains a menu, some links and a destination page which this test asserts to exist in the end. This is a very simple test indeed, but the point is to get started and to keep things simple later.

Tools for this tutorial are SeleniumIDE, Java, JUnit, WebDriver and Maven. The final code and configuration is available in github TODO: Link

### Recording the test case ###

Assuming that the functional tests are written to test existing features it may be efficient to record the test body using SeleniumIDE. Writing the test code from scratch is another option. The approach depends on how modular the application pages are. If the application uses components and has strict html structure, then writing tests by hand might be more efficient. However since most applications have more relaxed html structure, the tests might as well be recorded. At least it is a good way to get started quickly.

SeleniumIDE tutorials cover the recording process, so I will not repeat it here. But there are some principles and pitfalls to note.

While making this tutorial I encountered a problem with the default link locator. Locators are a mechanism to find elements on the web page. Link locator fails to locate the anchor that has line breaks in it's text. The locator works fine in SeleniumIDE, but fails to find the same link in WebDriver, which is what we use in the final Java. For this reason I went through SeleniumIDE options and reordered the Locator Builders so that xpath:link locator builder has priority over the link locator builder. Below is a screenshot of the Locator Builders option page in SeleniumIDE.

[![SeleniumIDE option - Locator Builders](/img/simple-functional-testing-with-browser/SeleniumIDE option - Locator Builders.png)](/img/simple-functional-testing-with-browser/SeleniumIDE option - Locator Builders.png)

After the test case has been recorded and functions properly in SeleniumIDE it is time to export it as Java code.

### Exporting and running the JUnit code ###

SeleniumIDE exports the test case in unpolished Java code. I used the option to export the test in "Java / JUnit 4 / WebDriver" format.

The code is raw and has "generated" look all over it, as expected. However it is good enough for a starting point. After some simple fixes it is runnable and should produce identical results with SeleniumIDE.

To run the code I wrote a maven Project Object Model for it.



### Refactoring the project ###

### Issues that need attention ###
- Locator problem with links that contain linefeeds