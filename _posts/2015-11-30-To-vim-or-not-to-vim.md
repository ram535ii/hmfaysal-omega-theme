---
layout: post
title: To Vim or not to Vim
description: ""
headline: "That is the question"
categories: technical
tags:
  - geeky
  - web-development
comments: false
mathjax: null
featured: true
published: true
---

So the title of this blog post is slightly inaccurate and that is that it implies that there might be a good argument to "not Vim," but it was just too good not to use. From the perspective of a humble Vim user there literally cannot be. The thought of having to use an IDE, for whatever reason that might be, and having to convert back hurts. But seriously, Vim might not be for everyone - so if you have to "not Vim" - do so proudly. Destroy that Sublime Text configuration!

I only joined the 'elite' cult, well in the eyes of my own kind, of Vim users very recently. I put elite in quotes because like every Vim user I love preaching Vim, but at the same time I love observing the hilarity of someone like myself actually caring so much about a text editor on an emotional level. I have many friends who also aspire to join, but how? The learning curve is so ridiculously high. You can't let your productivity at work drop too much just to learn this tool. This is my attempt at explaining the best way to convert. This won't work for everyone, but that's kind of the point - do what works for you.

And now for that useful stuff. I've broken it down into a few separate 'steps' and 'principles.'

# Step 1: Git commit like a pro
In my honest opinion everyone should use git through the terminal (you can already see the Vim running through my veins). If you don't, this is the perfect time to start. Why do I say so? The perfect place to get used to the very basics of Vim without totally disrupting your work flow is when writing commit messages. This is the time to learn what the different modes are: normal, insert and visual. This is the time to learn how to save and quit. This basic comfort provides the foundations for everything else. I spent literally years doing this (granted it was because I hated nano passionately, but see where it got me).

# Step 2: Find a Vim support group
You know how sales people try to convince you that purchasing their product is a win-win situation - your life is 'better' and they make hella cash. You need to look for a Vim-Vim situation - someone who will symbiotically help you. Luckily this shouldn't be too hard. A side effect of the preachiness of the church of Vim is that most addicts will happily spend ages explaining things to you. They literally get joy out of seeing someone else's interest in the tool. For me this was my awesome co-worker [Ed](https://github.com/seddy). As it was for me, and I imagine it will be for many people, this is the step where you can actually start using Vim fulltime. I think this support is super important because initially you will face lots of small, frustrating hurdles and keeping that frustration in check when you have to basically learn how to walk again is hard. Later on, as you learn you will actually learn from one another and that's where the fun really begins.

# Step 3: Pair with your support buddy
This is obviously a lot easier if you work together, but pair program with your support buddy. This is a great opportunity to see Vim in action and aspire to doing what your buddy is doing. While you're driving, you have the ideal co-pilot to not just help you code, but also tell you what crazy combination of keys you should be using to do something more effectively or just how to do something altogether. A lot of the features I use on a daily basis now I had not even considered were possible. Without pairing, it would have taken me so much longer to find them as well as learn how to actually use them.

# Step 4: Be awesome!
I think this is a pretty obvious step.....

Now on to the guiding principles, things that make life right and ways to keep your head raised while learning.

# Principle 1: Fuck the purists
Vim extremists are those people who insist that there is one 'right' way to use Vim. These are the people saying you aren't using it right if you use the mouse or if you use the arrow keys to navigate instead of 'hjkl.' They may be right in that this is likely the most efficient way once you are a pro, but starting this way is like jumping in the boxing ring with Mohammed Ali on your first boxing match - you're going to get hurt bad, run away and never come back. All the things that keep you going and make the experience good, just keep doing them - it's fine. For me, enabling the mouse in all modes was definitely one of those. As I said, do what is right for you. Only you can be judge of this, so no extremist can tell you what to do!

# Principle 2: Your .vimrc is personal
Your .vimrc is where all your settings live, all the customizations, all the little things you like. When starting off it seems like the easiest way is to grab somebody else's massive fuck-off .vimrc and just use that. Don't do that. You won't have any idea what any of it means and ultimately there will be a ton of stuff in there that probably isn't even relevant to you. Start with a blank file and add in the raw basics - such as enabling the mouse, line numbering, etc.

Life in Vim revolves around plug-ins, so there are a few I would say are essential to get started. Before diving in, you will need a method to handle plug-ins. I use [Vundle](https://github.com/VundleVim/Vundle.vim), a great plug-in manager. There are other options, such as [vim-pathogen](https://github.com/tpope/vim-pathogen), just use whatever works for you! The few actual plug-ins I could not imagine using Vim without, and I recommend you getting, are:

- [NERD Tree](https://github.com/scrooloose/nerdtree) - file tree navigator
- [Ctrl-P](https://github.com/kien/ctrlp.vim) - fuzzy search
- [Ag](https://github.com/rking/ag.vim) - The Silver Searcher in Vim

From here on out, just add other plug-ins as and when they are useful, as well as any other configs they require.

# Prinple 3: Symlink and version
Assuming you make it this far you will have already put your heart and soul into Vim. You will know your own configuration intimately, but not intimately enough to memorise it. So my advise is, version that shit! This is a tip straight from my Vim support buddy. The best way to do this is to move all your config into a folder, say `scripts` and then symlink the files into home, `~/`, as required. If you aren't familiar with symbolic links, [here](https://kb.iu.edu/d/abbe) is a great explanation. Now you can version your scripts folder with git, remember commit using Vim! In case you think this step isn't worth it - it is. It has saved my ass already and is also a great way to go back when you've royalled fucked something when trying to set up that "cool, difficult thing."

You should now be set for the road to coding nirvana. There is one more thing I feel obliged to quickly mention. Some people find a printed [vim cheatsheet](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html) useful. I had one, but didn't really use it. I just wrote all the stuff I couldn't remember on sticky notes. If you are interested in seeing my .vimrc or scripts folder - you can find it [here](https://github.com/ram535ii/scripts).

I would love to hear if people actually found this interesting/helpful, so feel free to ping me!
