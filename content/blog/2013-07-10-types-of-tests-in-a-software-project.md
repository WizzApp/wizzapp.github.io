---
title: "Types of tests in a software project"
date: 2012-07-10
tags: [software development, practices, automated tests, automated testing, integration tests, unit tests, acceptance tests, definition]
RedirectFrom: blog/2013/07/10/types-of-tests-in-a-software-project/*
---

### Disclaimer

The following descriptions and definitions are purely based on my own experience and knowledge. People will disagree. So be it ;-). I'm willing to talk about every definition in this post.

### Types of tests

1.  **Unit test**  
    Typically automated, this kind of tests exercises a single method in a system. In unit tests all external dependencies are mocked so that the tested code is completely isolated. Isolation in this case leads to a test that runs purely in memory as accessing a database of the filesystem would make this an integration test (see below).

2.  **Integration test**  
    Normally automated as well this kind of test does test a set of components and their interactions and their integration into the whole (thus the name integration test).

3.  **Acceptance test**  
    An acceptance test is another kind of integration test. Its goal is to verify that specific acceptance criterions (which are usually specified on a user story) are met when implementing a specific story.

4.  **User interface tests**  
    User interface tests drive the system through its user interface. Integration or acceptance tests may do this through special interfaces or on a layer just below the UI but a UI tests usually simulates a real user interaction like clicking a button or selecting an item in a dropdown.

### It's all just words

Those are the types of tests that come to my mind at the moment. There are more and there are also other names for some of those tests above. Also the definition varies from developer to developer (and that's good ;-). Nevertheless at least inside of a team a common vocabulary should be used for specific test types.

I hope this definitions help a little.
