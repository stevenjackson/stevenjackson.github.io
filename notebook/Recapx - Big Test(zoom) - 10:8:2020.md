Frontside
-----
Charles Lowell, Jonas (yo-nus) Nicklas(capybara), Taras Mankovski, Robbie Pitts, Min Kim, jrlainfiesta, 

TD
Todd, Steve, Grosz, Jack, Dan Kubb, Daniel, Kerry, Neal, Dustin, searls, Joel

# Big Test
Test-as-data framework
Cross Platform

## Why Big Test
There are small tests, medium tests, big tests (not unit, integration, system)

Big Tests are higher fidelity.
Bigger tests cost more - speed, reliability, realness

How do we attack those costs?

## Alternatives
Jest - Good DX, reliability, good for unit tests, terrible for big tests (rendering)
Cypress - balanced - ok at DX (slow), reliability (still a bit flakey), size - but isn't great at things that aren't browser based
Selenium - Good at large tests (coverage), not great at anything else.  

*What if we could have the speed of jest, tooling of cypress, coverage of selenium?*

# Demo

- Big Test Server
- Chrome agent
- Application is a black box
- Just going to a URL

## Test structure
- Arrange, act, assert
- Steps and assertions fully separated
- examples are nested as child (shared parent setup, ala rspec)
- If parent assertion fails, no child examples run - only one failure for an early issue rather than a screenful.

## Error output
- Didn't find the submit link, but we did find all these other links (Home, Sign Up, Sign in)
- Focus on providing useful error messages for quick developer interactions

# Details
* Does this use Puppeteer? No, we use web driver to launch the browser and then execute everything via html events
* Can run multiple agents - run the suite against chrome, iPad, etc.
* Server is graphQL
* All state is queryable - any past runs
* Interactor (things you can touch on the page) have async/dom event waiting built in (based on capybara experience)
 * The tests are not scripts, they're values.  Data.  Declarative.  The DSL just helps you build a tree.
 * Tests are portable and syntax independent.  
* The server knows everything about the test before it runs it.  How many children, branches, etc
* Arrange/Act/Assert is the only way
* Enables parallel assertions, branching, etc
* Divides the test tree into lanes, run the minimal number of steps
* Each lane can be isolated
* Build your own interactor for your special flavor of a Select component
* The server/orchestrator talks to distributed agents.  Because it's just data, the whole thing can just be sent to the agent.  No need to run each step of a script (aka selenium).
* Only web for now, but there's nothing stopping us from creating an iOS/android/Raspberry pi/node agent.
* TypeScript first for IDEs
* Discord link for questions


 
How is this faster? - Strict separation of steps and assertions - tests are just data that can be split.
Working on 1.0 beta.


# Questions:
## How much of the DOM is available outside the error output?
## Seems like breakpoints aren't an option because it's not a script?
* You can write a function that gets called from step and hits debugger


## Is the immutable functional style too big a leap?  Scripts are easy to reason about.  How do we do weird async stuff?
You can use drop into async/await syntax and get out of the declarative space

## How do you handle test pollution in the system under test?
* We recommend folks write full stack tests that are stateful
* But we don't handle backend state.
* Mock the backend for SPA
* Build an API to clean the database or build this fixture or whatever
*

## Syntax for custom assertions?
* Part of bulding the interactor

## What browsers are supported?
* Targeting evergreen browsers for now.  IE 10/11 probably possible (needs polypill), IE9 would be a challenge.

## Any support for timings/what's slow
* Not yet, sounds good

## Is there a product behind it?  
* Open source
* It'd be great if cypress could pick up the agent development
* Might enable products in the future - we'll be able to collect data about your tests
