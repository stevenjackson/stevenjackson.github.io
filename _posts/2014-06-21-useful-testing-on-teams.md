---
layout: post
title: "Useful testing on teams"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I was reading Uncle Bob's [article about TDD and teams] and like so much Uncle Bob writes, I find myself nodding furiously in agreement at one sentence and shaking my head at the next.  This quote caught my eye: "If each member of the team does what is right in their own eyes, without considering the values of the team; then they don't actually comprise a team. Instead they will behave chaotically, and work at cross purposes to each other."  While I can guess what he intends by that, what I hear is "the team must conform".

It seems obvious to me that rules and guidelines that work well in one situation can be misused in another.  I can easily create an extravagant example of greenfield code, completely TDD'd from the first second.  I could spend days demonstrating "proper" TDD technique and mostly write good tests that I'm solidly ok with.

The problem seems to be that I rarely work in new codebases.  Does anyone?  After the first release, some code (even TDD'd code, sorry Michael Feathers), is legacy.  It does what we wanted it to do 18 months ago, but we don't want it to do that anymore.  One thing I vehemently buy into in the agile mindset is that I WANT my product owner to violently change the software at a whim.  I want to provide value, and I want to do it every time.  If this isn't providing value anymore, it has to go.

Imagine some new trivial request.  We have a PaymentProcessor and we need it to send an extra parameter to the accounting system.  Luckily we already do this in other places.  All we need to do, to make this work, is change the call to that service.

If you're pairing with me at this point, I apologize.  To any sane person, the thing to do is to modify the one call.  15 second change, right?  Unfortunately, my brain won't accept that.  We're TDD-ing (yay us!) so we need a test for that.  You write a test that mocks AccountSystem and verifies the method is now called with the new parameter.  I cringe.  My brain is saying:  "That's not much of a test."  I pontificate for some time on how that test is a white-box test and isn't providing much value.  You reasonably ask for an alternative and I start to suggest something that verifies AccountSystem used that parameter.  You correctly point out that a test like that is brittle, since we're now digging into another object's responsibilities.  I sigh and agree to the original test.

This bothers me at a fundamental level.  I don't want to create unnecessary work.  I don't want to write brittle tests.  I don't want to write an integration test for every kind of change.  I don't want 9000 tests that assert the same thing coming from different starting points.  I don't want to write tests that test I know how my mocking framework works.  I don't want to write tests that don't test anything.  I don't want to write tests that aren't useful.

Have you ever written jasmine tests that pretty much just verify jquery works?  The thing that upsets me the most about these tests is that they never catch the mistake I make most often, which is screwing up the css selector.  The test that seems useful is a test that verifies "When I click this checkbox, radio button over there is disabled."  In order to pull that off I have to load a real page or write a ton of  mock html (that will quickly become obsolete and contain all the same typos I would put in the test).

I have a basic "rule" that I don't write unit tests for error messages.  In my experience, error messages are either "write once, forget forever", or they change on a weekly basis.  Either way the unit test isn't getting me much.  I also dislike tests where we make sure this field exists on a model or an object responds to a method.  "But wait", you might say, "the system relies on that method being there!"  And that might be true, but I won't take that test seriously when I decide to delete said method.

Unfortunately, my rule about useful tests seems to be, "Did I have to put any thought into that test?"  This scares me a little bit, because perhaps it implies that I only value work that stimulates intellectual creativity.  Unfortunately, I often have days where I NEED a network of stupid tests to catch my stupid mistakes.

One thing that helps a bit is writing the stupid test if that feels like the thing to do.  I don't know how to get started without a test like this.  I need a test like this to force me to call that method.  That's test-first as it's intended I think.  Let's use this cheap, simple tool to get the immediate feedback we need.  But I'm not sure those tests should live past their initial usefulness.

I used to work with a fellow who would pseudocode his methods first.  He wrote detailed, conversational comments of what this thing should do, in this order, for this reason.  And once he had his thoughts spelled out, he could write wonderful expressive code.  I copied this technique for a time with one key difference.  I deleted those comments when I was done.  I didn't like the noise of leaving all my thoughts out there on the page.  I appreciate a good copyedit here and there.  I feel like I could do a better job on my tests in this regard.

Then that fear strikes again.  Delete a test?  Reduce my test coverage?  Shrink the safety net?  "Waste" time deleting a test that does its job and "perfectly" documents how the code works?

I wish I had a good answer for all these conflicts.  It always comes back to "it depends".  And this is why I have such a hard time with the notion that a team should conform to a certain style of testing.  People grow, teams evolve, and code gets messy.  What worked for us last year may not work anymore - we need to be able to grow without being shamed for writing/skipping this test.  Unfortunately I rarely take this stance on a team.  I conform.  I do it because it's the easy thing to do.  I do it because I'm so often wrong when I'm sure that I'm right.  I'll suck it up.  I'll copy/paste/hack the terrible test that originally came from someone who wasn't sure how to test this thing and came up with `it { should respond_to }`  And I'll wonder, what sort of example am I leaving behind?

[article about TDD and teams]: http://blog.cleancoder.com/uncle-bob/2014/06/17/IsTddDeadFinalThoughts.html
