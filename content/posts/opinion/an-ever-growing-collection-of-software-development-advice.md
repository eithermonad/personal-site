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

## On Coding Against Interfaces and Dependency Injection

> This is a quick overview. To learn about Dependency Injection in full, see my article [A Practical Introduction to Dependency Injection](/2020/12/a-practical-introduction-to-dependency-injection/).

"Dependency Injection" - it sounds complicated. Three natural questions arise - "what's a dependency?", "what does it mean for a dependency to be injected?", "why would I want to inject a dependency?"

If some class `A` relies on the functionality of a class `B`, then `B` is a dependency for `A`, or, in other words, `A` holds a dependency on `B`. Consider a `UserService` class using the functionality of an `EmailSender` class. In that case, `EmailSender` is a dependency for `UserService` - `UserService` **depends on** `EmailSender` to function correctly.

It's pretty clear that dependencies are not a rare thing. In fact, it's common for a class to have many dependencies, and that's not a bad thing (so long as relevant principles like SRP aren't violated). The problem, though, comes from how you manage those dependencies. The concept of a dependency introduces the idea of relationships between classes, and relationships can cause different levels of coupling. The two partners of `UserService` and `EmailSender` are collaborators - they collaborate together. How said collaborators collaborate determines how much an application will resist change and resist testing.

If `UserService` instantiates a new `EmailSender` in its constructor, then calling code for `UserService` has no control over how the `EmailSender` is managed, nor can it swap out the `EmailSender` for a different kind if the business migrates or for a fake in a test case. We can solve this high degree of coupling and invert control back to the caller by only permitting `UserService` to receive an instance of an `EmailSender` into its constructor instead, and not create the `EmailSender` itself.

This, then, answers the second question and third questions - passing an instance of a dependency into a constructor (or through function arguments, we don't have to restrict ourselves to classes) is what it means to inject that dependency, and the reason we do it is to reduce coupling and give control back to the caller.

The issue that probably comes to mind, at this moment, is if `UserService` expects the type of the injected dependency to be `EmailSender`, then we still have high coupling because it means we have to pass an `EmailSender` in. We can't pass in a `FakeEmailSender`. We've solved the creation side of things - the lifetime management side, but not the fact the dependency remains too rigid through the type system. This is where interfaces come in.

Consider the notion of powering a toaster. You, the user, need not have any understanding of electronics to figure out how to run current through the toaster and heat the filament. Similarly, you need not worry about the max current that can be pulled through the socket, the voltage potential between live and neutral, what the frequency of the AC current is, what current draw over what time period will cause a breaker to trip, or even what the source of the electricity is.

Really, the only thing you're concerned about is inserting the plug into the outlet. If the plug doesn't fit, then you have a problem - maybe you're trying to use a European plug in a North American outlet and need an *adapter* (this is a design pattern), but, for the most part, the functionality is plug and play. The electricity source and the individual wires behind that outlet can change as much as it wants, but never will that affect your ability to place the toaster in the outlet so long as the outlet never changes. Another way to look at is you can swap the toaster for another toaster, a microwave, a kettle, or anything without the wall or wall wiring have to change. The outlet is the interface - it's agnostic to any concrete implementation of electricity or appliance, and it merely defines behavior (current flow) - not concretions, but **behavior**.

By defining an interface like `IEmailSender`, you're freed to create concrete implementations such as `SendGridEmailSender : IEmailSender` or `FakeEmailSender : IEmailSender` (that's `SendGridEmailSender implements IEmailSender` and `FakeEmailSender implements IEmailSender` for Java and TypeScript developers) that implement the interface. To implement the interface means to have the behavior as defined in the interface.

Interfaces can go hand in hand with Dependency Injection because now you can depend upon abstractions and not concretions. You can inject some email sender that honors the `IEmailSender` interface into `UserService`, and `UserService` doesn't need to know what it actually is because it knows what behavior is possible/provided thanks to the interface.

> This was a quick overview. To learn about Dependency Injection in full, see my article A Practical Introduction to Dependency Injection](/2020/12/a-practical-introduction-to-dependency-injection/).

## On Language Proficiency and the Preservation of Commonalities

Rather recently, I heard someone say that when working with various programming languages, they attempt to maintain and preserve commonalities - "mannerisms" - between those languages. For instance, they stick to classes as much as possible in JavaScript as to maintain a similar feel to Java and C#, and that this helps them easily move between languages rapidly.

This is an atrociously flawed mindset, the implications of which are fairly obvious. If you constrain yourself to utilizing the features shared across all languages, you effectively lock yourself to the least common denominator. There no longer becomes a reason to pick one programming language over another, for all will act just the same to you. The intersection of the set of features between languages will grow ever smaller with the more languages you attempt to add to the mix.

This idea of preserving commonalities is one that I can understand if coming from a new developer. They may not be viewing programming languages and technologies as *mere tools* quite yet, and they are likely moving between learning different languages with no clear direction, rhyme, or reason. This issue likely stems from a new programmer thinking that the more languages they add to their tool belt, the better a developer they become, when, in fact, the opposite is true. Learning only for the sake of learning, while not a bad thing in and of itself, tends to produce mindsets like these. Instead, a beginner should pick a language based on their interests, excel to a reasonable level of proficiency with that language, and then move on to a new one as required, taking advantage of the full scope of features that each language has to offer as they go.

I'm certainly not saying that learning for the sake of learning is a bad thing, just that having a *reason to learn* often makes for an easier and more streamlined learning experience. But deciding to learn the basics of Java, then the basics of C#, and then the basics of JavaScript simply makes you a software developer who knows nothing of real substance about 3 different languages when you could instead aim to reach a level of relative proficiency in just one said language, the knowledge of which will be easily transferable to the other two when such a transfer is needed.

That last point is what makes mere surface-level knowledge across an array of languages nowhere near as valuable as proficient-level knowledge of one. With the exception of static and dynamic typing and functional programming, most languages are actually pretty similar to one another, thus even the advanced concepts of a language like C# will prove somewhat helpful if you need to learn Java or JavaScript. Asynchrony, for instance, is a generally language-agnostic concept that is, most unfortunately, often taught within the context of a specific one, but you won't hear about asynchrony if basic data structures and control flow is the limit to how far you get dividing your time across N languages. If you had stuck with only C#, knowledge of C#'s asynchrony features would serve you well when making the move to JavaScript.

## Changelog

**February 27, 2021 at 11:47 PM CDT (05:47 AM Zulu):**
- Added section [On Unit Testing](#on-unit-testing).
- Added section [On Language and Framework Superiority](#on-language-and-framework-superiority).

**March 3, 2021 at 12:03 AM CDT (06:04 AM Zulu):**
- Added section [On Coding Against Interfaces and Dependency Injection](#on-coding-against-interfaces-and-dependency-injection).
- Added section [On Language Proficiency and the Preservation of Commonalities](#on-language-proficiency-and-the-preservation-of-commonalities).