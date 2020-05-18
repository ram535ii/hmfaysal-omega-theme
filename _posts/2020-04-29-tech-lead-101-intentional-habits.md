---
layout: post
title: "Tech Lead 101: Be intentional about habits"
description: ""
categories: technical
tags:
  - geeky
  - techlead
comments: false
mathjax: null
featured: false
published: true
---

Welcome to post eight in "Tech Lead 101", if this is your first one I'd recommend the [introduction]({{site.url}}/technical/tech-lead-101-intro) first. Check out the [table of contents]({{site.url}}/technical/tech-lead-101) too.

----

In my [previous post]({{site.url}}/technical/tech-lead-101-if-not-writing-code) I alluded to coding being a great opportunity to lead by example. In this post I’d like to dive into that underlying idea a little bit more.

You want to influence the behavior and standards of your team - whether it is how you run rituals, what you deem high enough quality in code or something totally different. One of the easiest ways of doing this is simply to show by doing, both giving an example and signalling what your expectations are. This is what I mean by leading by example, illustrating how you think something should be done by visibly and intentionally doing it yourself. When you do this, your team is learning through osmosis, just by seeing, engaging and frankly copying. Note, this is not micromanaging or telling someone else how to do it. Eventually the things you do will be so normal they are second nature to the whole squad.

This approach has one fatal flaw - you can’t use it to set the bar for everything you are going to care about, there’s just too many things. In line with that it's useful to remember that your goal is to enable your team, not do their job for them, so this is also the goal of leading by example. What I mean by all this is that you need to choose the _few points_ that you deem most important and focus on those. The way I do this is by being intentional about my habits.

I’ll use a personal example to illustrate this. There are a few things I care disproportionately about, both relative to other things and other people, as a software developer. The first is code comments that explain _why_ something is being done a certain way when it is of specific importance. Another is detailed pull request descriptions combined with a self-review before asking someone else to take a look. I believe it is important for my team to do this, so when I write code I am vigilant to make sure I do both these things consistently and to a high level. I’m equally vigilant on reviewing code according to these themes and praising them when I see them. The net result - every team I do this in ends up emulating this behavior in their code and their reviews, the bar rises. Needless to say, there are significantly more things I care about, but the list of things I intentionally do in this fashion is very small. I’d rather we do the most important ones really well than many of them averagely well.

In summary - choose the few things you deem most important, repeatedly do them to the highest standard as you play your role in the team and before you know it they’re normal.

This subject is one I’ve had numerous great conversations about in the last few months and I know other leads who also do this to great effect. I’d like to shout out a few more that I’ve seen work super well.

- Good commit messages: this one is top of the list because in the first conversation I had about this subject the other lead I was speaking to mentioned this habit - one I’ve done embarrassingly badly in the last years. Just that conversation prompted me to now be much more diligent with my commit messages.
- Always including tests: this one is maybe slightly less absolute, but setting the expectation that you include tests or explain in the PR description/commit why you’re not including them means it’s always an active decision.

You’ll notice that all these examples are technical in nature. This isn’t to say that they have to be, but this is where I’ve found this technique particularly effective. It’s also where wearing the tech lead hat truly shines, as _often_ you are uniquely qualified within your team to establish what is good enough.


----

{: style="text-align: center"}
[< If you're not writing code...]({{site.url}}/technical/tech-lead-101-if-not-writing-code)   -   [Write for your readers >]({{site.url}}/technical/tech-lead-101-write-for-your-readers)
