# Design notebook for week ending November 30, 2014

## Description

**TODO:** Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

**What questions do you have for your critique partners? How can they best help
you?**

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

* 45 minutes
  * Critiqued Ellen's project (still waiting for access to her GitHub repo, so I haven't posted the critique yet)
  * Still waiting for access to ELlen's GitHub repo... I've posted my critique below and I'll move it when I get access.

## Post-critique summary

## Post-critique reflection

## Critique for Ellen

In general, it looks like the project is going along well!

To me, it seems like user-defined relations shouldn’t be too difficult or frustrating to handle. That said, though, I could imagine a situation in which user-defined relations get incredibly complicated. For example, if you want to define something along the lines of “a granduncle is the brother of a person’s parent’s parent,” then the user-defined relationship is pretty complicated, as you’d need to store the conceptual model of the relationship. I think that’s probably more than you’d want to add. Adding simple user-defined relationships (in which there is no conceptual model other than the fact that two people are related) seems much more doable, though. I think the simplest way to handle that would be to have a generic case class that stores the two people and a string describing their relationship. So, you might have something like  `UserDefinedRelationship(Person("Jimmy”), Person(“Jenny”), “buddy”)`. You might also want to think about if all user-defined relationships are symmetric or not (and whether you allow the user to clarify this). I could imagine defining “buddy,” which I’d want to be symmetric, but also “mentor,” which I would not want to be symmetric.

I also have a few more generic comments from looking through your code. (These are just things I noticed; there might be more context behind why you did things the way you did. Definitely take all of this with a grain of salt.)
  * I think there might be value in representing either Child or Parent in the abstract syntax, but not both. Because `Child(p1, p2)` and `Parent(p2, p1)` mean exactly the same thing, it seems you could simplify your IR and your semantics by only representing one of the two in the IR. 
  * Is there value in representing the Self relationship? It seems so obvious that it need not even be implemented. (On closer look, it seems you might be using it because that’s the only way to represent a person as an edge in the list of edges. However, is there value in having a person without any relationships defined? Will your query language let you do anything with that?)
  * You might want to consider decoupling your query language from your specification language a bit more. Because they are so different, it makes sense that they should be separated as much as possible. For example, perhaps consider writing `eval_edge` and `eval_query` functions (which are called from `eval`) in order to divide the two distinct modes of operation as much as possible. (You could do a similar sort of thing in your parser by writing a query parser and an edge parser, then just having the main parser be `query | edge`.)
