---
title: "Comments Are Not Always an Anti-Pattern"
date: 2021-02-17T11:57:10-06:00
draft: false
toc: false
images:
tags:
  - comments
  - unit-tests
---

It certainly would not be erroneous to state that, more often than not, feeling the need to write comments implies a problem with underlying design - that the code itself leaves something to be desired. Code should be expressive and interfaces should be intention-revealing. If you get this right, you rarely need comments. The notion of behavior, not mere data, should be treated as first-class.

It would make sense, then, to extrapolate this idea and say that comment usage itself is an anti-pattern. But that, for reasons which should be quite obvious, is undeniably false. In fact, **the *biggest* anti-pattern of all is believing that some statement or idea applies to all situations unilaterally, without exception, and without limitation.**

While it is true that comments have the risk of becoming stale over time and need to be maintained along with the code, there are, in fact, I believe, a multitude of situations where comment usage is justified, primarily because comments excel greatly at providing information that is not expressible in code.

### Sacrifices for Performance

There may be small, rare cases where the performance requirements of an application dictate that readability must be sacrificed to maintain adequate perf. In such cases, comment usage is justified. Indeed, readability should seldom be sacrificed, but at the end of the day, design requirements must be fulfilled. You could have beautifully written and elegant code, but if the system doesn't work as needed, or if it doesn't function at the performance level expected, what's the point?

### Workarounds

There are generally cases where one has to take seemingly unjustified actions in code to work around a bug or handle an edge case. It is crucial that this be well documented, thus comment usage is justified (and required), perhaps even linking to relevant issue numbers, if any.

### English Explanations

Certain operations may benefit from English explanations - especially paradigms that not all developers are aware of. Functional Reactive Programming, for instance, where the dimension of time is implicit and all data is streamed, might benefit from a brief explanation. With that said, such an explanation need not be first-class in code, but a small one here and there doesn't necessarily imply issues with expressiveness. If anything, it adds to it. Concepts like these aren't always intuitive, can't always be understood no matter how expressive and intension-revealing the code might be (especially if they're fundamentally implicit, perhaps even philosophical in nature), and a comment is a small price to pay to avoid confusion.

A need for English explanations may also arise out of situations where code is performing operations that are heavily algorithmic or mathematical in nature, such as graphics, audio analysis/FFT, physics, etc. Namely, concepts beyond the scope of most developers who aren't specialized in the domain.

## When Comment Usage isn't Justified & Why Reliance Should be Placed on Tests

In almost all other cases, comment usage does indeed imply that code should be refactored to express the meaning that once only existed within the comment. During refactoring, the meaning once implied in comments should manifest itself within the code based on proper naming, emphasis on behavior, the Tell Don't Ask principle, and, crucially, unit tests. 

Saying that a unit test only exists to validate a given behavior is equally erroneous as stating that comments are always an anti-pattern. There is another crucial piece of value provided by tests that isn't always taken advantage of - not only do they verify behavior, they tell stories, they provide insight into logic and the domain.

Test suites should be written such that a developer can gain all the insight he or she needs into the codebase by reading the story that the tests tell, be that through scenarios like Given/When/Then or Arrange/Act/Assert. Writing expressive code in the first place plus having expressive test suites to fill in the gaps should remove both ambiguity and the need for comments entirely except in those cases listed above. Heavy procedural flows generally attract comments, for instance, when they can be perfectly explained in tests.

## Conclusion

Everything is situational. Use comments when comments will add value. That's it. But don't use them in lieu of or as an excuse for going without expressive code and expressive test suites.