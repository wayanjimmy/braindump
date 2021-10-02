+++
title = "Real Programmers Commit to Master"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Real Programmers Commit to Master - Jakob Ehn](https://youtu.be/hL1OZfgoZGk)

related
: [Talks]({{<relref "20210511121448-talks.md#" >}}) [Git]({{<relref "20210217134705-git.md#" >}})


## Background {#background}


### Long live(d) Branches {#long-live--d--branches}

-   Big bang merge, hard to resolve


### Feature Branching {#feature-branching}

-   Create a new feature in a feature branch
-   Other development keep on master
-   2 or 3 team working on their feature branch at the same time
-   It seems like a good idea because we can select a new feature when it comes to deployment
-   It's hard to test combination of 2 or more feature branches
-   What about refactoring? continous improvement work in the way


### Trunk Based Development {#trunk-based-development}

-   Everybody works on master branch
-   Release from master, or from short-lived release branch
-   Branch only short lived
-   What about bug fix?
    -   Fix bug to the master, you only allowed to commit to master
    -   Cherry pick the fix into the release
    -   This is to avoid **regression** if you forget to merge the commit to master


#### Benefits of Trunk Based Development {#benefits-of-trunk-based-development}

-   Minimize merge work/conflicts
-   Encourages small batches of work
-   Encourages refactoring
-   Always release ready
-   Better delivery throughput


#### How to do this? {#how-to-do-this}

-   Small, incremental and compatible changes
    -   Everything going to master should be ready for release
    -   Every commit should be releasable
-   Use feature toggles for unfinished work, until is done
-   Push quality upstream (Shift left)
    -   Run unit test during code review to make sure the code going to master have high quality
-   Safe deployment techniques for minimizing impact
    -   Canary deployment?


#### Feature Toggle {#feature-toggle}

-   Glorified if-else statement
-   <https://martinfowler.com/articles/feature-toggles.html>
-   Put the Feature toggles on the top (UI) layer, why?
    -   It doesn't benefit you to **repeat** it else where, just creates technical debt
    -   Don't forget to **protect** your new endpoint

{{< figure src="/ox-hugo/feature-toggle-layer.png" >}}


#### Feature toggle implementations {#feature-toggle-implementations}

-   Launch darkly
    -   is it overkill? you get very nice dashboard, analytics, and A/B testing
-   [Flagr](https://github.com/checkr/flagr)
-   [Flipt](https://github.com/markphelps/flipt)
-   [Unleash](https://github.com/Unleash/unleash)
-   [Go Feature Flag](https://github.com/thomaspoignant/go-feature-flag)


#### Feature toggle considerations {#feature-toggle-considerations}

-   As few as possible
-   As high up as possible in your code, so you don't duplicate it, it can be a mess
-   **Remove** when done!
-   Use telemetry
-   Test all combinations?
-   Don't ship security holes


#### Shift Left {#shift-left}

Pushing quality in your code as soon as possible

check your quality as soon as possible

Pull Request is a great place, do code analysis, security checking, run unit tests, run everything before it hits master.

Add policies to the master branch to make sure everything check, example:

-   Every PR should be reviewed


#### Testing Pyramid {#testing-pyramid}

You have a lot of unit tests

Integration to test API

UI to test a feature

and Manual testing

but the reality it's not pyramid, more like an ice cream


#### Shift Left at Microsoft (DevDiv) {#shift-left-at-microsoft--devdiv}

-   Nightly Tests ~22 hours

-   Full Automation Run ~2 days

-   Tests failed frequently

-   Failed tests often ignored until the end of the sprint

Principles:

-   Tests should be written at the lowest level possible
-   Write once, run anywhere including production system
-   Test code is product code, only reliable tests survive
-   Testing infrastructure is a shared Service
-   Test ownership follows product ownership

Test Taxonomy:

L0 Fast in memory, < 60ms
L1 Might require assembly + SQL or the file system, < 2000ms (avg 400ms)
L2 Run against "testable" service deployment
L3 Require full deployment. Run against production

The greater the number, the more the external dependencies

L0, no dependencies and fast
L1, unit tests with dependencies, because it hits database
L2, functional test executed on deployed systems
L3, test full deployment in production (almost impossible have a staging environment that reflect production)

Read more: [Shift Left make test fast reliable](https://docs.microsoft.com/en-us/devops/develop/shift-left-make-testing-fast-reliable)


#### Safe Deplyments {#safe-deplyments}

Rollout new version incrementally

-   Canary releases
-   Dark launches

    Separate deployment from release, you don't have to deploy and release for every user at the same time

    Automated release gates, try to remove manual tests


#### Canary Releases {#canary-releases}

Divide your user to several groups

1.  Canaries
2.  Early adopters
3.  Users

Read more : [How Microsoft Deployed Windows 10 Inside the Company](https://www.zdnet.com/article/how-microsoft-deployed-windows-10-inside-the-company/)


#### Dark Launches {#dark-launches}

Like canary release, but the feature is invisible to end users

Test a feature in production without the user actually noticing it

Often used for backend changes that could have large impact
