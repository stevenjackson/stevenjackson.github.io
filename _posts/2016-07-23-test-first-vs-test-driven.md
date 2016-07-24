_includes/themes/the-program/post.html_includes/themes/the-program/post.html---
layout: post
title: "Test-first vs Test-driven"
description: ""
category:
tags: []
---
{% include JB/setup %}

Why am I bringing back an argument that no one has had in years?  Well, I've spent quite a bit of time reflecting on #whyitdd and how it differs from other people I've paired with.  Recently, I heard Corey Haines on Ruby Rogues and he made a new observation that made me tweak my thoughts a little bit.

As I mentioned in [TDD is a Path](http://stevenjackson.github.io/2014/01/26/tdd-is-a-path/), I started TDD a long time ago as the only developer writing unit tests on a larger team.  It was mostly a frustrating experience, but I still felt like it was "the way", if only because I had been thoroughly brainwashed by all the blogs and books I was reading.

More recently, I had the opportunity to work on a project where most of the developers were in their first or second job out of college.  They TDD'd because that was the way they were taught and they had no frame of reference for any other way.  This was pretty fascinating to me, they were doing things "the right way", but if you dug into their reasoning it was just dogma.  We do it this way because we do it this way.  In my mind, they were test-first developers, but not test-driven.  They wrote the tests first because they were supposed to, but they had already settled on the design in their head.  My gentle prodding to just write the test and see what happens was hippy nonsense as far as they were concerned.  We got to the right places, but they were pretty sure that I had the map all along and just strung them along until we got there.  That was mostly flabbergasting to me, I had been preaching and converting for so long that when most of the team was saying what I wanted to hear I couldn't believe they weren't doing it for the purest of reasons.

I've long believed there's a difference between test-first and test-driven and that it had something to do with existing code and new code.  With existing code, I want to make sure I'm not breaking anything.  So I'll put some tests in place to give me confidence that things aren't broken.  Tests that tell me what the rules of this universe are.  With new code, I'm not terribly concerned about safety, I'm focused on what a solution might look like and how I can make it suck as little as possible.

But what I've found is that many of the people I pair with really are concerned with that safety and correctness; in their mind there's really no other reason to write tests at all.

There's a chasm between appreciating the tests and actually putting them at the same level as the production code.  And the conflict rears it's head when the production code design feels pretty good, but the tests just suck.  DHH's "TDD is dead" hammered on this for awhile, with the idea that TDD leads you to bad design.  If the tests "force" you to "compromise" the design, then you're viewing testability as a second-class citizen.

It now seems obvious when we talk about this and questions like "is TDD a design tool?" that we've conflated test-first with test-driven.

One mindset is about safety.  These are the benefits of "TDD" that initially drew me in.  No bugs, quality baked in.  Tests as documentation.  Safety net.  Repeatable.  Keeps code clean.

Another mindset is about discovery.  I crave feedback about this thing I'm building.  I want to understand how clients will use it.  I want to change it often as I discover new things.  I want change to be easy.

Now I don't want to come across as saying test-discovery is "better" than test-safety.  They're both tools and I think either can work based on your mindset.

These sort of things happen when I'm in a Test-safety mindset:
* I keep writing edge case tests that pass (because I've already designed for them)
* I change one line of production code and 20 tests fail
* I hack out a solution and then surround it with tests
* I avoid libraries because they don't have unit tests
* I write or move tests because a refactoring puts the code in a different file
* I'm focused on making code that is correct

These sort of things happen when I'm in a Test-discovery mindset:
* I slice the problem into one test at a time
* I write unit tests during a spike
* I throw away tests because I don't need that feedback anymore
* I write multiple versions of the same test to find a name or abstraction
* I'm focused on making code that isn't painful to use/maintain
* I end up some place I didn't expect

I think it's interesting the way my attitude shifts based on the environment at the time.  When I'm anxious about a solution or a timeframe, I'm working from a place of fear.  I don't necessarily want to discover a better way to do anything, I just want to get it done and have it stay done forever. On the other hand, when I feel like I've written this plumbing logic before, I might be more incline to riff a little bit and see if there's a better way.  When I'm test-discovery, I feel like I can go far and I can go fast.  I'm building a little narrow bridge to a new place.  Maybe everyone can't follow me, but that's ok, I'll figure out if we want to go there first.  When I'm test-safety, I'm building robustness.  Here's a nice concrete highway for a million other people to travel on.  Programming languages matter here too.  When I unit test in java, I find myself writing tests to prevent anything the compiler might allow.  Here's a function that adds a list of ages.  Hmmm...what if these ints are negative?  When I moved to ruby, I threw that mindset away.  You can do anything you want, and testing for negative inputs makes as much sense as testing for pepperoni pizza inputs.  I think something similar might happen with more experienced teams.  I'm not going to test for everything, because you have some responsibility not to go too far outside my intent (which is hopefully captured well in my tests :)  YAGNI starts to apply.  And if you don't need those tests for safety, maybe you start feeling like they're holding back your ability to discover as well.

I often say, if we're still focused on TDD in 30 years, we have failed as an industry.  We need to keep trying different things to find better ways to get feedback, better ways to express intent, better ways to make code simple, better ways to make code safe, better ways to change rapidly.  What's out there that's better?
