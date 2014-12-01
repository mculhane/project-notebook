# Design notebook for week ending November 30, 2014

## Description

This week, or team worked completely independently. Because we did not have our standard team meetings and because our schedules were so constrained by the Thanksgiving break, we just tackled completely different aspects of the project. Christine and Nick wrote the preliminary evaluation document (which I also read over afterwards). My main focus this week was on improving the parser and the semantics. In particular, I added basic recurrences to be parser. In order to support this functionality, I also had to add a new case class called Every to our intermediate representation. (Our initial design documents already called for this case class; we just didn't need it until now.) I also did a lot of brainstorming regarding the semantics (particularly the semantics of task completion and recurrences).

As part of my work this week, I spent a lot of time thinking about the semantics of recurrences. What follows is a rough summary of some of the main issues I considered.

My large brainstorming session spawned from a thought about how recurrences would actually be handled. In particular, we had previously discussed that a recurring task could be treated as a generator of sorts, which would yield individual tasks. We had also discussed, though, that a recurring task would be treated as one task (which is the next-due instance of the recurrence). While these approaches seemed to be different ways of thinking about the same general idea, it's clear now that they're not. The simplest example is the following: If we have one recurring task and we ask for the next 10 upcoming tasks (sorted by due date), what is the appropriate output? Should we get one task (representing the next-due instance of the recurrence) or ten tasks (representing the next ten instances of the recurrence)? We need to make a decision about how recurring tasks should behave before we can answer this (and that decision will affect a lot of how the semantics of recurrences works). There's also the question of how we should handle recurring tasks without both a start date and a due date. (I think that considering just one next-due instance of a task is probably best, especially considering that we might want to support cases like tasks that recur after another task is completed, for which it is hard to project out into future instances of the recurrence.)

Task completion also raises some issues we haven't considered. Because we support dates such as "2 days after task A is completed", we need to record when a task is completed. Would this be too much to tack onto our one-line syntax? If so, we would need to move to a multi-line syntax. If we do this, the compactness of our single-line syntax would seem particularly strange (and it might make sense to go to a multi-line syntax). We also need to consider task completion for recurring tasks. Is it sufficient to store the completion details for the most recently completed iteration of a task, or do we need to store completion details for every instance? 

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I think the most pressing issue is to figure out the semantics of recurrences. As part of my brainstorming (which is more or less summarized above), I realized that there are a lot of cases that we haven't thought about too carefully. It will be important to resolve these issues before the semantics are meaningful and useful.


**What questions do you have for your critique partners? How can they best help
you?**

Because we weren't critiqued last week, my question about syntax remains. During our in-class test, we got some feedback
that our one-line syntax (see our sample program) is very confusing and difficult. We were interested in building a syntax that balances clarity with speed of typing (because a todo list that takes forever to create is pretty much useless). That said, it's tough to tell if we struck the right balance. Some feedback on this would be very helpful.

Also, it would be helpful to get some feedback on how we might want to handle task completion, especially for recurring tasks.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

Due to the Thanksgiving holiday, I put in substantially less time than normal this week. In particular, because I do most of my work for the course over the weekend and because our team typically has Thursday and Sunday meetings, all of my standard work time was taken up by the break. Therefore, the amount of work that I completed is less than normal. That said, though, I did make some progress this week and look forward to getting fully back into the swing of things by next week. I will also do whatever I need to do to ensure that the project is completed by the time it is due.

As described above, we worked independently this week due to the break. My focus was on improving the parser and semantics. I made some improvements, but I also spent a lot of time brainstorming.

* 45 minutes
  * Critiqued Ellen's project
  * The critique was completed on time, but submitted a few hours late (as I was still waiting for access to Ellen's GitHub repo).
* 2.25 hours
  * Completed project notebook, added recurrences to parser and IR, and did substantial brainstorming regarding the semantics of recurrences (which is partially summarized above).

## Post-critique summary

Our project was not critiqued this week.

## Post-critique reflection

Our project was not critiqued this week.
