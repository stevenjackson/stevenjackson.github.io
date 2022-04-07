https://engineering.shopify.com/blogs/engineering/shopify-monolith

> A single centralized team can’t make change happen by working against the momentum of hundreds of developers adding features.

Ability, Motivation, and Prompt - Fogg Behavior Model

Easy to do, motivated to do it, and reminded to do it.

> Pushing for consistency added rules, which always add some friction, because they have to be learned, remembered, and followed. It didn’t make any hard problem significantly easier to solve.

> We’re focusing on finding the areas where developers are hungry to make positive change, but don’t end up doing it because it’s too hard.

> looking for areas where the prompt is easy, the motivation is present, and we just have to amp up the ability to make things happen.

<DANGER> We currently have 37 components in our main monolith, each with public entrypoints covering large parts of its responsibilities. Packwerk is used on about a third of the components to restrict their dependencies and protect the privacy of their internal implementation. We’re working on making Packwerk enticing enough that all components will adopt it.

