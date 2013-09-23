---
layout: post
title: "Legacy Code Refactoring"
description: ""
category: 
tags: []
---
{% include JB/setup %}

#### Summary:  I'm disatisfied with my feedback loop while refactoring larger pieces of legacy code.  What can I do differently?

So I've tried to explain a phenomena to a few people lately and I keep falling flat.  I can only conclude I'm explaining it badly, or it's a solved problem that I haven't seen the solution for.

So imagine some legacy code.  My most recent example was a chunk of a few thousands of lines in a class spread across a handful of methods.  Pretty much status quo for this app, but this was particularly painful because it was a huge chunk of the business rules for various validations.  There was temporal coupling, where half the code was basically ignored under some conditions.  This caused some issues when we'd go to add new checks - it wasn't apparent that this 1200 line chunk was effectively dead code under normal operations, because the coupling was enforced three layers up.

So we did our due diligence and got most it under test coverage.  At least to the point where we felt comfortable pulling at it a bit.

It's hard to describe test-driving a change where the "wrong" solution is already in place.  Here we have 6 years of tweaks and pokes of fairly complicated code all dumped in the middle of an even larger class (this logic is probably 5% of the total class size).  It's a big, awful, mess.  I had two goals in mind:

1.  Make the temporal coupling explicit
1.  Put a fence around this minefield

So here's where I have trouble explaining what happens.  Here I have a chunk of code.  I want to change it safely with small refactorings.  So I make a small change.  Run my tests.  Repeat for hours/days/whatever.  Unfortunately, unlike "normal" TDD - I'm not getting feedback on design direction.  I'm running my tests constantly and staying green, but I have no idea that this idea for trying to pull out a class is a good one.  Or that changing the return value on this method helps in any way.  

I think part of the problem in my explanation is that I'm saying "refactor" but I'm really talking about "re-design" in a significant way.  Refactoring a class is easier to think about; hopefully I can wrap my mind around all the relevant parts and keep seeing the simple steps forward.  This is still refactoring in the application sense, I don't want to change it's behavior.  However I do often want to change how several classes work together to simplify the design.  With TDD that's easy (for me), I just listen to the tests.

Normally in TDD I can listen to my tests.  If the setup is excruciating for a test case I can see where it needs to change.  If the assertion is complicated, I can see that I'm probably testing via the wrong method.  If I'm copy/paste/hacking chunks of code around, that's an alarm that I'm making this too hard to understand.  Tests provide great FAST feedback on design decisions.  I detect obvious seams and can see where my classes are taking on too much responsibility.  I can make little experiments very quickly and get that fast feedback where a first class collection worked well here, but introducing this value object didn't clear much up.

With this case - we have a ton of painful tests.  Think about how many unit tests we needed to cover all the conditional complexity in this example.  I'm completely immune to this pain - I just spent days sucking it up to get the code under test.  And I don't want to change these tests - they're now my safety net for future change.

So yes, I make my changes.  I run my tests.  I keep the bar green.  But I'm not getting anywhere.  I might spend hours gradually building the wrapper for this code and plumbing it through the layers.  Just to find that it won't work because X.  Or it's making things worse!  Some abstractions just don't work.  How many code bases have I dumped a new idea into that didn't take off?  Too many code bases are swamps of vestigial tails.

I've only stepped away from one of these sessions twice feeling like I'm now "ok" with this code.  *That* problem won't haunt my dreams forevermore.  The first time I was extremely lucky.  Everything just worked, I focused my chi, I was guided by the Muses - just one of those "zone" experiences that only seem to happen at the rarest of times.  Generally I fail/fumble my way to a solution - I tell myself it's the scientific method.    I have no idea how to reproduce this miracle, I took small refactoring steps as I'd prefer to, I just always picked the right one that led to a simpler solution.

The second time I essentially started test-driving the solution from scratch.  I built the whole thing up again, using the existing tests as my guide.  And then I had a big-bang switchover where I drove the new solution with the old tests before deleting those monstrosities forever.  And that sucked.  First there was the process of doing 4x the work of just getting it under test in the first place and hacking something together.  Then there was the problem that the new solution was completely worthless until it was done.  Then there was the integration step at the end.  Back to the bad ol' days of pulling it all together at the end and wondering why it didn't work.

I've tried to detect places where you can split the big ball of mud and test-drive those into smaller-bang switchovers.  But I seem to pick the wrong splits to keep my old tests working and still move towards a better design. I usually don't know what that design is - that's why I want to test-drive it!  In this case we were just trying to get it all into a single terrible class.  And we couldn't figure out how to get there from here without breaking everything.  Twice.

Every other time, I've tried what seems like the safe route.  Get it under test.  Refactor the obvious stuff.  Hem, haw, and pontificate.  Get burned out and move on to something else.

There has to be a way to handle this problem.  If not, we're screwed, because code like this isn't going to be wished away.  These stopgap temporary projects always seem to last for decades.

Any ideas?
