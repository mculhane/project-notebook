# Design notebook for week ending November 16, 2014

## Description

This week consisted of several team meetings in which we finalized our plans for the intermediate representation and extensively discussed our plans for the semantics and computational model of our language. Much of this discussion has been memorialized in the Language Design & Implementation document, which we wrote collaboratively.

I also spent a few hours working on a first pass at our semantics. The work I completed this week includes support for dependencies, but not recurrences. I plan to add support for recurrences early next week. While working on the semantics, I realized that it would not be possible to simply duplicate the exact structure we used for our Scala projects. In particular, Python does not have algebraic data types or pattern matching like Scala does. Given this issue, I initially decided to go with more of an object-oriented approach in which each class of the IR was responsible for its own functionality. This decision came with its own set of issues, including the fact that it closely coupled the IR and the semantics (which we would like to avoid). Ultimately, then, I decided to mimic the Scala functionality in Python by using standard Python classes/inheritance (we don't need any of the special features case classes provided). To mimic Scala's pattern matching, I decided to check the type of each object. This is distinctly unpythonic, but it does seem to get the job done. We'll need to discuss this decision in greater detail when we next meet as a team.


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I think the most pressing issue is to confirm my general approach to the semantics. More specifically, we need to confirm that the approach I've taken is superior to an approach in which the functionality is built into the IR classes (which it likely is). Furthermore, we should probably confirm that our decision to develop the semantics in Python (in order to have easier interaction with Sublime) still makes sense over using Scala (and then having to do more work to get the Sublime plugin functional). Much of my thinking this week about how to structure the semantics was based on the Expression Problem we discussed in class.

**What questions do you have for your critique partners? How can they best help
you?**

Does the general structure to the semantics/IR seem appropriate? Do you have any suggestions regarding how we might simulate (or avoid using) pattern matching, or does our current approach look okay? Is the approach of checking types to simulate pattern matching so unpythonic and cringeworthy that we should avoid it?

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

We worked collaboratively in our team meetings. Towards the end of the week, we split our work into three parts: syntax (Christine), semantics (me), and Sublime Text plugin (Nick).

My work log for the week is below. I have only include time spent out of class.

* 0.75 hours
  * Critiqued Nick & Christine's work
* 1 hour
  * Team meeting, worked on language design & implementation document
* 3 hours
  * Team meeting, completed language design & implementation document (amid significant discussion about the contents of that document)
* 2 hours
  * Team meeting, had a Scala vs. Python discussion, played around with case classes in Python (ultimately deciding to do without them), completed first draft of simple IR
* 2.5 hours
  * Worked on first pass at semantics (without support for recurrences, just dependencies), fleshed out project notebook for the week

## Post-critique summary

Christine had two main points in her critique. First, she emphasized that development of an intermediate representation should be a priority in the project. Second, she suggested that the Sublime Text plugin should be more than just a wrapper on top of our syntax. Rather, she thought that it would make sense for the plugin to provide a more GUI-like interface for adding, editing, and managing tasks.

## Post-critique reflection

I think both of Christine's points are really useful. This week, we completed the intermediate representation, which will allow us to develop the syntax and the semantics of our language independently. (In fact, we prioritized a preliminary version of the IR during one of our team meetings so that we could easily split the remaining work.) I also agree that a GUI-like interface in the Sublime Text plugin would make for a cleaner user experience, so it would certainly be a nice addition. Those additional features are not absolutely central to our language, though, so I would guess that a more robust task entry/editing interface would be something that we would tackle as a stretch goal near the end of the project (if we get to it).
