+++
title = "Learning Angular as a Java Developer"
author = ["Shweta Kadam"]
date = 2023-03-03T23:03:00+05:30
tags = ["angular", "typescript", "guide", "blog"]
draft = false
+++

Recently got an opportunity to work on angular project.With no previous experience in angular, I had some catch up to do in terms of web development.So here is a small blog post.


## What is Angular ? {#what-is-angular}

Framework to build client side applications.


## Why would you use Angular? {#why-would-you-use-angular}

Vanilla JQuery code gets harder to maintain,harder to test.

And like all most of the frameworks Junction, Angular provides:


### Angular gave our applications clean structure. {#angular-gave-our-applications-clean-structure-dot}


### Includes lots of Reusable code {#includes-lots-of-reusable-code}


### Makes the application more testable {#makes-the-application-more-testable}


## Also easier to co-relate to learn from Java perspective because of 2 features {#also-easier-to-co-relate-to-learn-from-java-perspective-because-of-2-features}


### Dependency Injection {#dependency-injection}


### Typescript {#typescript}

gives our plain JS applications some structure &amp; enables static typing.


## 3 Handles Server-side Rendering {#3-handles-server-side-rendering}

We don't save the data in client. We save it in server. Example:  Data is wiped clean when user creates form.

Frontend Backend           --&gt;     Backend
(Presentation logic)                Data APIs Business

Let's get familiar with some terms in Angular first. Below is small comparison to co relate between Java and angular.

| What                       | Java          | Angular                               |
|----------------------------|---------------|---------------------------------------|
| Dependency management      | Maven         | npm(node package manager )            |
| Build/package              | Maven         | webpack                               |
| Library  Repo              | Maven Central | npmjs.org                             |
| Project Descriptor         | pom.xml       | package.json                          |
| Programming language       | Java          | Typescript ,HTML                      |
| Platform runtime           | JVM           | Browser/NodeJS                        |
| Unit Testing               | Junit         | Karma/jasmine                         |
| Reactive Programming       | RxJava        | RxJS                                  |
| Code style checks          | Sonar         | eslint                                |
| Browser End-to-end testing | Webdriver     | Protractor (Layer on top of selenium) |

Like java has a main file. Similarly in angular, there is a `main.ts` file which is the starting point of our application.It is present in bootstrapmodule(Appmodule).


## Webpack {#webpack}


### Angular uses a tool called `webpack` which is a static module bundler.It takes all our HTML,CSS and JS files and bundles them into a single file which is loaded by the browser. It bundles application source code into convenient chunks, to improve performance and load times. {#angular-uses-a-tool-called-webpack-which-is-a-static-module-bundler-dot-it-takes-all-our-html-css-and-js-files-and-bundles-them-into-a-single-file-which-is-loaded-by-the-browser-dot-it-bundles-application-source-code-into-convenient-chunks-to-improve-performance-and-load-times-dot}


## Hot Module replacement {#hot-module-replacement}

Hot Module Replacement (HMR) is a feature of webpack that allows developers to update code changes without the need for a full page reload.
When a code change is made, HMR only updates the module that has been modified, which means the application can continue running while the changes are applied.
