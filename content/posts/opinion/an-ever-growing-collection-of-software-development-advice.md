---
title: "An Ever Growing Collection of Software Development Advice"
date: 2021-02-27T00:38:10-06:00
draft: false
toc: true
images:
tags:
  - unit-testing
  - software-development
  - software-architecture
  - repository
  - orm
  - adapter-pattern
  - dependency-injection
  - frameworks
  - advice
  - opinion
---

This article marks the home of an ever growing list of random software development advice, mostly covering architecture, mannerisms, principals, and practices. It is updated regularly and you can see the [Changelog](#changelog) at the bottom of this page for more details.

## On Unit Testing

Work in Progress.

<!-- A generally erroneous but still all-too-prominent *practice* when writing unit tests is to rely heavily on mocks and mocking frameworks. Specifically, this issue seems to stem from an equally erroneous and equally all-too-common *idea* that the definition of a "unit" in a "unit test" is a single function or class. The aforementioned practice follows logically from that idea - if the unit is the function under test and only the function under test, you can't possibly allow logic within external dependencies used by that function to influence the results of the test. As stated, this is false. Many will say that a unit test requires the mocking of all dependencies while an integration test allows the inclusion of dependencies. -->

## On Language and Framework Superiority

It's rather pervasive, especially among members of the web development industry, to consider certain languages, frameworks, and libraries as supreme to others - in some cases going as far as to say that said language, framework, or library is the best in the world.

Such blanket statements are inherently erroneous and speak to the inexperience of the person making the statement.

At the end of the day, all languages, frameworks, libraries, principals, patterns, mechanisms, and architectures are *merely* **tools** - they exist solely as a means to an end, as a means to get the job done. Depending on the situation, one tool may be better suited than another to get that job done, but that never implies that said tool is in any manner "supreme" to the other(s) outside of that situation.

It's important to understand that everything exists within a given context - all that ever succeeded did so within a clearly defined context, and everything that ever failed did so within an equally clearly defined context. Pick the tools that best fit the context within which you wish to use them.

The specific criteria for tool selection that arise out of a given context aren't always strictly technical in nature - generally, political and logistical considerations have to be factored in, and it's up to you to decide how to balance the two. The priority of feature completion (time-to-market), the current skills and operating scope of the team, the performance requirements of the solution, the weight assigned to maintainability and the minimization of future technical debt, the community and ecosystem around the tech/tool, and more should go into deciding upon a specific tool, not the preference of the developer or development team.

This sounds rather quite obvious, and, alas, it probably is to most. With that said, I all-too-often see and hear people publicly declare their favorite technologies and tech stacks and state that they use them for every project or every requirement, which is asking for trouble.

Since I often hear this from some members of the web development community, I most generally see JavaScript, Node.js, and MongoDB held up to very high esteem and applied (erroneously) unilaterally across contexts. Just because you *can* use JavaScript on the front-end and the back-end doesn't mean you *should*. That said, it doesn't mean you *shouldn't* either - decide based on the context you're operating within. Similarly, just because there are methods of programming Microcontrollers with JavaScript doesn't imply that that's a good idea either - it just means the possibility exists. The same goes for MongoDB - most domains are inherently relational, and trying to represent such data in a denormalized manner won't always work out well (not that there aren't use cases for document storage forms - there are).

Additionally, undue hate, negativity, and insults toward technologies follow naturally (unfortunately) from the designation of other technologies as supreme. For instance, you most often hear people make fun of C#, Java, and PHP as being old, legacy, out of date, reserved only for enterprise use cases, and too hard to work with. None of this is true, and the hilarious thing is that many of the people who make such statements have likely never worked with any of these, and instead merely jump on the bandwagon. The fact of the matter is that C#, Java, and PHP are great languages, have their use cases, and *do their jobs very well*, just as JavaScript does its job well.

Just like you wouldn't attempt to use a Phillips screwdriver in all scenarios just because you "prefer" it to flatheads, don't try to utilize technologies in all situations either. **If you have to massage the tool to fit the use case, then the tool isn't the right tool for the job.** Let the needs of the project - both technical and political, your existing experience, the size and maturity of the community and the ecosystem around the tool, and any other relevant criteria govern technology selection. In doing so, you can make decisions through a purely objective lens.

## Changelog

**February 27, 2021 at 11:47 PM CDT (05:47 AM Zulu):**
- Added section [On Unit Testing](#on-unit-testing).
- Added section [On Language and Framework Superiority](#on-language-and-framework-superiority).