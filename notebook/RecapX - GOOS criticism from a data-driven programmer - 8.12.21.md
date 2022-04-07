
https://dpc.pw/growing-object-oriented-software-vs-what-i-would-do

> but the belief that iterating itself without any upfront design idea leads anywhere, is in my opinion nonsense.

Oooh - this feels really important.  If I'd never experienced just TDDing my way to a solution, then I could see where I would think this is impossible.  It feels really similar to the opinion that pairing/mobbing could never work in "the real world" - there's a suspension of disbelief required to even get out the door.  And then several _years_ of being bad at it after that.

>When writing a program like this, my first and most important consideration would be data model design 

And then he immediately hits the opinions that fit a personality I've paired with.  There's some notion that you have to know _what_ will be transported before you can figure out _how_ to use it.  I think that's false, but not intuitively so.  It's obviously easier to have a static schema to start from, so the opinion leans towards  putting all our energy towards building that first.  In the meantime we have absolutely nothing that can demonstrate value because we're still modeling and configuring kafka.

I'm sort of reminded of Stephen Vance's scrum talk, where he spent a lot of time building out the context.  GOOS reacts to a world where we often tried to figure out all the data and reqts up front and always broke everything when we decided we'd adapt the software made for selling cars into something that can rent them as well.  The idea that we just won't worry about the schema and it frankly it isn't terribly important leads towards a very different kind of design.