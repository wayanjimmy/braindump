+++
title = "The definition of Refactoring"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Learn go with tests]({{< relref "20201208202033-learn_go_with_tests" >}})

link
: [Mocks and tests are still making my life hard](https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/mocking#but-mocks-and-tests-are-still-making-my-life-hard)

The definition of refactoring is that the code changes but the behaviour [stays the same]({{< relref "20201208152000-preserving_behaviour" >}}).

If you have decided to do some refactoring in theory you should be able to do make the commit without any test changes. So when writing test ask yourself:

-   Am I testing the behaviour I want, or the implementation details?
-   If I were to refactor this code, would I have to make a lots of changes to the tests?
