---
layout: post
title: "Tech Lead 101: Write for your readers"
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

This is the ninth post in a series which starts with the [introduction]({{site.url}}/technical/tech-lead-101-intro). The [table of contents]({{site.url}}/technical/tech-lead-101) lists all the posts.

----

Why write, but for it to be read? The title of this post borders on the tautological because it’s so obvious. Yet in many cases we find ourselves writing without the reader of our work clearly in mind. We could deal with this subject in the abstract, as it applies so widely, but I’m intentionally going to frame it within the job of a software engineer, to make it more relatable.

Let’s start off by identifying exactly why this is so important. Consider all the following statements:

- Code comments are for those reading your code longer after it is merged
- Pull request comments are there to serve the pull request author.
- Pull request descriptions are there to enable the pull request reviewer.
- Technical design documents (we call them “proposals” at Monzo) exist to garner feedback from reviewers and guide engineers once building.
- Documentation is almost so self explanatory I didn’t include it.
- Slack messages serve no purpose if not to communicate with their readers.

Even code itself is there to be read. On the surface it’s job is to solve a problem or provide some tangible value, but it can only do that if the people working with it can read it.

With all these examples in mind, I’d posit that if you’re going to do any writing without the intention that it serves your reader, then why write at all? This is of course a somewhat flippant assertion. In reality it can be surprisingly difficult to remember this in the moment, particularly because writing well is by no means obvious or easy.

So how do you actually write with your reader in mind? There is no easy fix here, though interestingly I’ve often found that the simple act of reminding someone to write for their reader is enough to get meaningfully better writing. I genuinely recommend trying that, it may be the highest impact thing in this blog post, but let's also look at some other things to think about.

**Who are you writing for?**
Knowing your audience is half the battle. If you are commenting on a pull request by someone new to your company, you may need to go into more detail. Code comments will be read by both your most junior and senior engineers, so if you write just for the latter you’re doing a dis-service to the former. If a document is being written to share within your team, you can probably assume a lot more context than if you’re circulating it much more widely.

**Don’t assume context, unless you’re certain you can.**
If the point above is the “who” of writing for your reader, this is the “what.” You may need to adjust your content to provide additional context, context that is in your best interest that the reader knows to fully understand your writing. Is there a proposal I should have read before reading this code? Is there some industry best-practice you’d like to take for granted. If you’re not totally certain that your readers will know something, it's better to say it or link to it. It’s kind of another way of saying that you should know your audience.

**How do you write?**
This may be the point you thought this entire post was about. How do you use the literal words you write and where they’re written to their full potential? One could probably write a book on this. Replace acronyms unless they are industry standard. Don’t use big words where small words will do - I mean why would anyone use the word “tautology” in the opening word of a blog post like this!? Use diagrams liberally. Use color. Consider neuro-diverse audiences (e.g. if color matters, consider contrast). Space things out. Use bullet points. Avoid long sentences. Use headings. Keep things simple.

You may have noticed that all these points refer to each other. If you were to resolve all those references you’d just be left with one big point, which is - write for your readers. It is of course circular to say that you write for your readers by writing for your readers. I’m not quite sure exactly where to start either, but that doesn’t mean you can’t just start by doing lots of small things more intentionally.

Remember, even when writing for yourself, write for the reader, because that reader is you. Whether that “future you” is a few hours from now or a few years, it’s almost always worth it. I’ll admit, when I’m writing a proposal, before a first draft is done, it is selfishly written for myself as the writer. I use the document to develop my own thoughts. I think this is fine. It's just once you start sharing it or commit it to being read much later, the point at which it needs to start communicating, that the reader becomes important.

I can hear you think, but this is a series about tech leading, why did I just read all that? Honestly, because you’re in one of the best positions in your team to remind people - whether it is by making it an intentional habit and leading by example, giving conscious feedback or just talking about it every once in a while.

----

{: style="text-align: center"}
[< Be intentional about habits]({{site.url}}/technical/tech-lead-101-intentional-habits)
