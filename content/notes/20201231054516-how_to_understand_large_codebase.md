+++
title = "How to understand large codebase"
author = ["Wayanjimmy"]
draft = false
+++

link
: [HackerNews: How to understand large codebase](https://news.ycombinator.com/item?id=16299125)

related
: [Git]({{< relref "20210217134705-git" >}})

You can use the debugger on low level api calls to get pretty much anywhere in the codebase. If you want to find whats changing a label to "foo" you can hook into every set\_Text call and put a conditional breakpoint on all label changes to break on "foo", then just go up the callstack to find the logic. This strategy works on network interfaces and file interfaces as well. I abused this on our 2M+ SLOC legacy codebase and it has saved me many hours. `=Also use version control to identify the most commonly edited files in the project=`. These are usually the files that are doing all the work (80/20 rule) and you likely need to know of them.

```sh
git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```

This strategy takes time, but it works really well:

1.  If you can, get an overview from a mentor. This will make the next steps a lot easier. Get: - history - philosophy - design style - high-level flow
2.  `=Get a stack of white paper from the printer and put it in front of you along with a pen.=` Colored pens and scotch tape are a bonus (There may or may not have been a shortage of both printer paper and colored pens next to them when I started at my last job)
3.  `=Open a debugger with a breakpoint=` on the first line of code
4.  Pick a request flow and initiate a request. Let the debugger guide you through the entire request flow
5.  `=Record the path of the flow as a sequence diagram on your paper=` `=( BONUS ) Record the relationships between the components in the system in a class diagram=`

Why does this work? There's software out there for making these diagram, so why draw them by hand? For most people, visual memory is the strongest. So, the idea is you use your strong visual and spacial memory to assist you in recalling random objects, facts. And hey, why not a codebase? And that's why this works. When you look at different files that the debugger guides you through, you are engaging your visual memory. You remember how the code is organized and what the files look like.

When you draw the `=sequence diagram you engage your spatial memory=`. E.g., the Router class doesn't interact with the Database class and so they are one sheet of paper apart. Visually, you can see what clusters of components work together to make larger structures. This allows you to mentally group the classes into a single concept.

The point is to get this information into your head, and not to produce a diagram on a piece of paper. If all you need is the latter, use software, of course. Seriously, when you're done, throw away the piece of paper; it will be outdated the next day anyway.
