---
title: "An Ever Growing Collection of Software Development Advice"
date: 2021-02-27T00:38:10-06:00
draft: true
toc: false
images:
tags:
  - unit-testing
  - software-development
  - software-architecture
  - repository
  - orm
  - adapter-pattern
  - dependency-injection
  - advice
  - opinion
---

This article marks the home of an ever growing list of random software development advice, mostly covering architecture, mannerisms, principals, and practices. It was last updated on February 27th, 2021 at 12:40 AM CDT. See the [Changelog]() at the bottom of this page for more details.

### On Unit Testing

A generally erroneous but still all-too-prominent *practice* when writing unit tests is to rely heavily on mocks and mocking frameworks. Specifically, this issue seems to stem from an equally erroneous and equally all-too-common *idea* that the definition of a "unit" in a "unit test" is a single function or class. The aforementioned practice follows logically from that idea - if the unit is the function under test and only the function under test, you can't possibly allow logic within external dependencies used by that function to influence the results of the test. As stated, this is false. Many will say that a unit test requires the mocking of all dependencies while an integration test allows the inclusion of dependencies.

