Waiters and Changers

@kentbeck

# Key Ideas

* Software Design is an exercise in human relationships
* Software Design: How to balance needs and investment for as long as possible
* 4 Levels of Software Design maturity

---

# Software Design is an exercise in human relationships

* Waiters - Have IDEAS - want behavior
* Changers - Make the changes

## Software delivery as-a pipeline
IDEAS go in -> Behavior comes out

### Changers view:

IDEA -> Behavior ----> Structure ----> Behavior

Waiters can't see structure - there's a curtain there.

### Conflict

* Waiters - "Why is this change taking so long?"
* Changers - "Everything is a mess!"
* Changer <-> Changer - "You keep breaking my stuff"

## Dysfunction 1: Optimizing for Behavior Change
* Initially Waiters are happy
* But things slow down
* Change slows as structure gets muddled
* But a precedent/expectations has been set - IDEA to Behavior takes X long

## Dysfunction 2: Get the structure right
* 2nd system syndrome
* "We'll get it right this time"
* Investment in structure is infinite
* Waiters never get the payoff, IDEA to Behavior pipeline stays slow

!! **Software Design: How to balance needs and investment for as long as possible**

# Maturity model
## Level 1
* Change stuff until it works!
* Deliverable: A big blob of quasi-related changes (system behavioral change)
* "I got it working!"

## Level 2
* There are 2 kinds of changes!
* Structural & Behavioral
* REFACTORING!!!
* Deliverable: A smaller? blob of structural and behavioral changes
* "I made it easier to understand"

## Level 3
* Playing Chess
* Make this structural change, then make this behavioral change
* Make this behavioral change, then clean up the mess
* Make the Change Easy, then Make the Easy Change
* Red/Green/Refactor
* Delivery: An ordered set of changes
* "That was easy to change!"

## Level 4 (experimental)
* Make each type of change it's own PR.
* A PR is either Structural XOR Behavioral

### Structural PRs
* Structural changes are reversible
* Review can focus on "aesthetics" and "direction" and ignore "correctness"
* Auto-revertible?

### Behavioral PRs
* Behavioral changes are often not-reverisble (can't take back a tax filing)
* Needs good tests
* Reviewer needs to be rigorous, think about consequences, verification, etc

### Hypotheses
* Multiple PRs that are only Structural or Behavioral allows the Changer to control the speed of delivery and establish predictability.  If the Waiter feels urgency the Changer can structure PRs to deliver Behavioral changes first.
* Delivering each individually provides more feedback opportunities (correctness, value)
* The Changer <-> Changer relationship will be improved.  Mulitple deliveries means more opportunities for feedback/correction/collaboration.

### Criticism
(mostly mine)
* Requires speedy review to feel like you're not waiting on that structural change to make the behavioral change easy.  But if they're truly refactors, maybe theres's a rubber stamping that's ok, knowing they're reversible. BUT if I stack a behavioral change on top, and the underlying structure is bad, I've lost my revertibility.  Maybe that's ok.
* I don't buy that Waiters would be satisfied with a world where we could order behavioral changes faster but choose to deliver structure instead.  We'd be making the same excuses as before - I can make this change you want easily if I spend two weeks cleaning up the models first.  Oh you want me to make it anyway and clean up later?  :shocked_pikachu:
* Counter-criticism - you think the guy who worked on the first XP project has any patience for "this new way of doing things can't work"?
