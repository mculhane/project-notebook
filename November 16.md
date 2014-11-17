# Design notebook for week ending November 16, 2014

## Description

This week consisted of several team meetings in which we finalized our plans for the intermediate representation and extensively discussed our plans for the semantics and computational model of our language. Much of this discussion has been memorialized in the Language Design & Implementation document, which we wrote collaboratively.

I also spent a few hours working on a first pass at our semantics. The work I completed this week includes support for dependencies, but not recurrences. I plan to add support for recurrences early next week. While working on the semantics, I realized that it would not be possible to simply duplicate the exact structure we used for our Scala projects. In particular, Python does not have algebraic data types or pattern matching like Scala does. Given this issue, I initially decided to go with more of an object-oriented approach in which each class of the IR was responsible for its own functionality. This decision came with its own set of issues, including the fact that it closely coupled the IR and the semantics (which we would like to avoid). Ultimately, then, I decided to mimic the Scala functionality in Python by using standard Python classes/inheritance (we don't need any of the special features case classes provided). To mimic Scala's pattern matching, I decided to check the type of each object. This is distinctly unpythonic, but it does seem to get the job done. We'll need to discuss this decision in greater detail when we next meet as a team.


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

**What questions do you have for your critique partners? How can they best help
you?**

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

## Post-critique reflection
