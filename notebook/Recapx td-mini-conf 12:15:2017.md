# Empathy, Boldness and Boundaries:
@marcpeabody

### Crucial Conversations

1. How to avoid crucial conversations?
1. What leads to them in the first place?

> If you're like this when you're ok, you're going to be kinda like this when you're stressed

* DNA matters, but we can't do much about it, so lets ignore it

## Be less Passive

### Passive Coping
 * Doing what is expected of us, maybe we don't like That
 * Sacrificing who we are to be another Person
 * Adds stress
 Fight or flight + passive coping = passive aggressive or passive flight
 violence or silence

### How to be assertive without being a @#$!$!
* Active listening - this is what I think your perspective is
  * Articulate so clearly, fairly, vividly that the listener
* State level of understanding and that you're aligned
* Avoid jumping into the rebuttal or criticism
* Build safe places to have conversations - create passive relationships, 1:1s etc so that these can be used later
  * How to build this into an engagement?
* Nervous about offending or being seen as ramming your opinion through
* This bothers me, I'm going to try to work on it not bothering me
* I'm not feeling good about this
  * But I might be willing to sacrifice this one time
  * If you don't say anything you're training them that this behavior is ok
* When you're being assertive - you're not listening - need to balance
* Being assertive takes practice, finding the balance takes practice

## Be more Passive

* Stress levels are based on perception rather than reality
* Life is different than expectations

#### Questions to ask
1. How does this affect my goals?
1. Will this matter in a year?
1. Should I say something?
1. Can this wait until later?

-----
kadams54 [9:41 AM]
Brian Dennett's full set of rules for critical commentary, from "Inituition Pumps and Other Tools for Thinking":

1. You should attempt to re-express your target’s position so clearly, vividly, and fairly that your target says, “Thanks, I wish I’d thought of putting it that way."
2. You should list any points of agreement (especially if they are not matters of general or widespread agreement).
3. You should mention anything you have learned from your target.
4. Only then are you permitted to say so much as a word of rebuttal or criticism.
-----

# Postgres is the best database
@neal

### INSERT
#### ...RETURNING
```
INSERT INTO people (first, last)
VALUES ('Neal', 'Lindsay')
RETURNING id;
```

Can also be used during UPDATE and DELETE
#### ....ON CONFLICT
```
INSERT INTO report_join(mgr_id, report_id)
VALUES(123, 456)
ON CONFLICT DO NOTHING
```
```
INSERT INTO extra_attr(person_id, att, val)
VALUES(123, 'title', 'Double Agent')
ON CONFLICT UPDATE SET val = 'Double Agent'
```
^^ UPSERT ^^

* Can also do multiple `ON CONFLICT` with different constraints

### SELECT

* Postgres has lots of aggregate functions - check em out

#### Common Table Expressions

* Move sub selects to the top of the query for readability
```
WITH
  foo(a, b) AS
  (
    VALUES(1, 'one'), (2, 'two')
  )
SELECT * FROM foo;
```

#### WITH RECURSIVE
* Build tree structures

```
WITH RECURSIVE
  mentors(id, name, mentor_id) AS
  (
    SELECT <BASE CASE>
    UNION ALL
    SELECT <RECURSIVE CASE> with INNER JOIN on common table expression (mentors)
  )
SELECT id, name, mentor_id FROM mentors;
```
```
WITH RECURSIVE
  mentors(id, name, mentor_id) AS
  (
    SELECT
      id, name, mentor_id
      FROM people
      WHERE id = 1
    UNION ALL
    SELECT
      p.id, p.name, p.mentor_id
      FROM people p INNER JOIN mentors m
      ON p.mentor_id = m.id
  )
SELECT id, name, mentor_id FROM mentors;
```

### text search
```
SELECT to_tsvector('I tried') @@ to_tsquery('try');
```
* A tsvector value is a sorted list of distinct lexemes, which are words that have been normalized to make different variants of the same word look alike
* A tsquery value stores lexemes that are to be searched for, and combines them using the boolean operators & (AND), | (OR), and ! (NOT). Parentheses can be used to enforce grouping of the operators:

### types
* Boolean
* varchar(n), text **DONT USE CHAR**
* int, bigint, serial, bigserial, numeric(precision, scale)
  * serial, bigserial - attaches a sequence to the value
  * numeric - fixed point ** NOT A FLOAT **
* timestamp with time zone, interval
  * `timestamp`does not have a timezone
  * `timestamptz` is the alias
* uuid
* inet, cidr, macaddr
* int8range, tstzrange
  * Take 2 timestamps, cast them into a range, run queries
* point
* line, lseg
* box, polygon
* circle


Does circle 1 contain circle 2?
```
SELECT
  circle '((1,1),1)' <@ circle '((0,0),5)';
```  

#### jsonb
Does the object on the left contain the object on the right?
```
SELECT
  '{"example": true, "concept": "containment"}'::jsonb @> '{"concept": "containment"}'::jsonb;
```

### LISTEN/NOTIFY

```
LISTEN foo;

NOTIFY foo, 'hey!';
```
* Tell actioncable to use postgres instead of redis and it will use this

Questions: http://is.gd/qs2jo1

# Tech Lead tactics
@kevin

Jerry Weinberg - Secrets of Consulting

## Sherbie's Three Laws of Consulting

1. In spite of what they tell you, there's a problem
1. No matter how it looks at first, it's always a people problems
1. Never forget they're paying you by the hour, not the solution
  * If you offer solutions that admits there are problems
  * When you're a good consultant, the client magically solves more problems
  * Bury your successes

#### Know your apps, domain, tech really well

#### Never stop being a programmer.  Never stop loving building stuff.

#### Only work on one thing

#### Don't be a slave to the process

#### Make an effort to avoid the first plans

#### Vary your retrospectives

#### Be obviously human.  Publicly show when you're stuck.  Be publicly vulnerable

## Any advice is good/bad based on context

# Jacob on Philosophy
@jacob

Our possible knowledge is contingent upon our conditions of possible experience

Antiquity -> Medieval -> Scholasticism -> "Enlightment" -> Modern(analytical, continental) -> Structuralism -> Post-structuralism

## structuralism
* Michel Foucault
* what makes thought possible?
* There's a structure built through opposing forces
* We can identify and change the structure that thought is based on

## post-structuralism
* Michel Foucault rejects structuralism for episteme
* Episteme: underlying epistemological assumptions that determine what is acceptable
 * epistemological - how do we acquire knowledge?
 * what are the currents and context that people are bringing to the environment

### Power is knowledge
 * Knowledge is ???
 * System of power is based on the knowledge of those "ruling" the system

### bell hooks _feminism is for everybody_
 * Doesn't use academic language
 * Very approachable
 * Analyze systems of power and change them
 * We live in a white supremacist, imperialist, capitalist patriarchy
  * The challenge of de-colonization - you're being forced to be like the majority
 * There is no process for liberation, it's about meeting concrete people/learning episteme, understanding the context and liberating them

### Anarchism
 * Todd May
 * Direct action
 * There are always a series of struggles along a variety of fronts
   * Not just capitalism, communism
 * A ground-up movement of free voluntary associations

## How does this apply to software development?

### Problementization
 * What's going on here?  How can I analyze this?
 * We determine what the problem is composed of
 * We create the problem through our "objects of thought"
   * X is being unreasonable
   * X and Y are using different languages
 * How am I defining the problem I see?
 * What words am I using?
   * These words structure the problem/solution space
   * Every situation has a context

### Friendship
 * Friendship is endangered in a capitalist society
 * Every individual is an entrepreneur that is competing for resources
 * Seek friendship - find someone with a common interest that will not further your career
 * Find friends that aren't like you
 * Friendship and community can fight systems of oppression

### Question systems of power
 * The people with power can change the system, they have to be convinced that they're oppressing
 * The people being oppressed must learn the system; they need to be convinced they can be liberated


# How to Pitch Test Double

### Farming is everyone's job
1. Identify problems at clients
1. Ask "Could Test Double help fix this?"
1. If no, don't sweat it
1. If yes, bring up idea with account manager
1. We'll create a team-based strategy for selling it

### Be a good team member
* "We wish we could clone $AGENT_NAME"

### What does Test Double do?
* Test Double is a premier agency
* that deploys senior developers
* to join our clients' teams
* and help them get things done with a high level of quality
* and once the team meets whatever velocity expectations they face
* we initiate our Secret Double Agent Mission(tm)
* of leaning back and asking hard questions about design, testing, and technical debt
* and fostering continuous improvement
* such that the team keeps making things better, even after we're gone

### This isn't a script
* We're not doing an elevator Pitch
* We're trying to build relationships
