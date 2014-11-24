# Design notebook for week ending November 23, 2014

## Description

This week's work was mostly focused on implementation (finally). After chatting extensively amongst our team and with Philip (our critique partner), we decided to implement our DSL in Scala (instead of in Python). We had already started an implementation in Python, but we decided to make the switch for a few reasons:
* Scala has several tools (parser combinators, case classes, pattern matching, etc.) which make development of DSLs easy. We found replacements for most of these in Python, but the replacements felt much more forced and inconvenient.
* We want to implement our DSL using the functional approach discussed in class. While Python has higher-order functions, Scala lends itself to functional programming by default.
* We thought that Scala's static typing would prove useful during development.

We split our work for the week into three parts: the semantics (me), the syntax (Christine), and the Sublime plugin (Nick). I ended up working on the syntax as well. For this week's work, we only focused on a very specific subset of our language. In particular, our two core features (dependencies and recurrences) are not yet implemented. We have implemented everything such that those features should be relatively easy to add, though.

For the most part, our syntax and semantics are similar in structure to those we used for the Piconot project. I did notice, though, that we needed a way to represent datetimes. I settled on (nscala-time)[https://github.com/nscala-time/nscala-time], which is a Scala wrapper around Java's Joda Time. (Joda Time is an improved datetime library for Java, which most notably makes objects immutable.)


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

At this point, I think our most pressing issue is just adding dependencies and recurrences to our
semantics and parser. Because those features represent the core issues we hoped to solve with our
language, we should probably address them soon. Other than this, though, I don't think we're
currently at any design/implementation roadblocks.


**What questions do you have for your critique partners? How can they best help
you?**

I think the most vague part of our language is still the syntax. We've developed the current syntax over the past week and we haven't given it nearly the level of attention that we've given our IR. What do you think of it? What do you like or not like about it? (A sample program in this new syntax is in the GitHub repository.)

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

As described above, Nick worked on the Sublime Text plugin, I worked on the semantics (and also a bit on the syntax), and Christine worked on the syntax.

The following is the time that I spent on the project (outside of class):

* 1 hour
   * Critiqued Phil's work
* 2.5 hours
   * Team meeting, worked on semantics (and studied Scala quite a bit to keep everything idiomatic)
* 3 hours
   * Team meeting, got parser mostly done, began writing tests
* 1.25 hours
   * Did some troubleshooting with the parser (got it working finally) and wrote some test cases
* 1.5 hours)
   * Improved error handling with parser, wrote (and tested) a sample program. (First example of syntax/semantics cooperating!)
   * Completed notebook entry for the week.

## Post-critique summary

There were two main themes in Phil's critique. First was that he had a lot of concerns with how we were implementing our language in Python. These concerns have been eliminated by our switch to Scala, though. He was also concerned about our plan for error handling in our language. In particular, he was concerned that it would be possible for our language to unintentionally interpret malformed programs (without handling them at the semantic level).

## Post-critique reflection

I think Phil had some very useful points this week. His thoughts about Python vs. Scala definitely informed our decision to switch to Scala (and we were also having many of the conerns that he listed). I also think that he's right to be a bit concerned about error handling. Error handling is admittedly an aspect of our language that we have not given a ton of attention to yet, so our plans there aren't very well fleshed out. That said, I don't foresee any major problems with error handling. We will need to make sure that we catch parse issues and surface them to the user in an easy-to-read manner. (We currently have some failure cases built into the parser, but they aren't yet working as intended.) Then, in the semantics we also need to put effort into making sure that we stop and surface an error to the user when an impossible or confusing situation occurs. For example, we can make sure that a task's due date does not occur after its start date. These sorts of simplifications and validations should be pretty quick and they would also help us avoid a number of basic user mistakes and cases for which the language's behavior is not intuitively obvious.
