# Design notebook for week ending December 7, 2014

## Description

This week, I focused on implementing dependencies and recurrences.
This involved major overhauls to the parser and semantics, as well as some
important design decisions.

In order to keep our language simple and useful, we made several
simplifications to the functionality of our language. Many of these changes
were made to avoid unclear and ambiguous semantics, and some were implemented
in the interest of time (as we'd like to end up with a functional language
by the end of the project). A list of the decisions we made (and the rationale
behind each one) is below:

* We added new syntax for tasks with dependencies.
    * `#AAAAAA Turn in completed assignment ^ #BBBBBB Due + 3 days, Start + 3 days`
    * The clear downside to this new syntax is that it adds more (admittedly kind of
      unclear syntax) to the language. If we were to undergo a syntax overhaul (which,
      frankly, would probably be useful), then we would design this a bit nicer.
    * The main benefit of this syntax is that it enforces a few decisions we've made:
        * By specifying the dependence (the task on which this task depends) only once,
          we prevent a task from depending on two different tasks. While there are certain
          cases where it might be useful to depend on two tasks (starting A after B and making A
          due before C), the semantics of this would get extremely confusing if either
          of the two dependences recurs (and especially if they recur at different intervals).
        * The start and due dates of a task that depends on another task must be defined relative
          to the start and due dates of the dependence. This means that a task with a dependence
          cannot have a start/due date that is just a timestamp. The reason we made this decision
          is that it is unlclear what should happen if task B depends on task A (which recurs weekly),
          but task B has start/due dates that are timestamps.
        * A recurrence can not be specified for a task with a dependence. This is because the
          recurrence behavior of the dependence will be inherited by the depending task. We made this
          decision because specifying a recurrence and then depending on a task with a different
          recurrence is confusing. (If A recurs weekly and depends on B, which recurs monthly, the
          expected behavior is unclear.)
* Recurring tasks must have a start date and a due date defined, and the recurrence interval must
  be larger than the amount of time which an instance of the task is active. (For instance, if a
  task recurs weekly, task.due - task.start must be less than 1 week.)
    * This decision was made for two key reasons. First is that it aids with implementation, as we
      can implement the semantics with the understanding that only one 
* We will only support recurrences of the form `every [quantity] [unit]` (such as "every 3 weeks").
    * We made this decision purely due to time constraints. In the future, it should not be too
      difficult to add a few more recurrence types. In particular, we would like to add "named" periods
      of time (days of the week, months, etc.). For example, in addition to supporting "every 3 days",
      we would like to support cases like "every Saturday and Sunday," "every February," and "every
      second Thursday of the month."
        * If we had time to implement these cases, we would require that a task's active interval
          (interval when it is active) is smaller than the interval of the recurrence. So, if a task
          recurs every Saturday and Sunday, we would require that the task's active interval be less
          than one day.
    * Our IR is constructed such that adding new recurrence types should not require too much extra
      work.

These changes and requirements have had the dual benefit of us allowing us to simplify our code
(particularly the IR and semantics) and clearing up ambiguous functionality. We decided that it would
be best to err on the side of disallowing certain behavior instead of making a choice about how the
semantics should work. We felt that it would always be unacceptable for the language to do something
other than exactly what the user intended, as every error in the language's behavior (or every place
where it deviates from the user's expectation) is an opportunity for the user to slip in their
obligations and lose trust in the language. So, we have constructed the syntax (especially the
new dependence syntax) to eliminate some ambiguous cases, and we will alert the user to others
when they run a program.


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

At this point, I think the mest pressing issue for our project is testing and polishing. We have
implemented all of the features that we will be implementing, and we now need to test thoroughly
to make sure that everything works as expected. This will also include introducing appropriate error
handling to make sure that the language fails gracefully when it encounters an error.

**What questions do you have for your critique partners? How can they best help
you?**

How do you feel about the design decisions I outlined above? Do they make intuitive sense, or do
they seem unnecessarily restrictive? Similarly, are there any other cases where you think there
could be ambiguities that we've missed?

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

We split this week's work into three distinct parts. (Because we had enough productive discussion
in class, we decided to forego team meetings this week and put the extra time into our respective
pieces of the project.) Nick worked on the Sublime Text plugin. (In particular, I believe he worked
on date parsing and syntax highlighting, as well as on "productionalizing" the plugin.) Christine
got a head start on the documentation for our final deliverable. (We will all be contributing to
this documentation in the coming week.) I focused on adding recurrences and dependencies to the
the parser and the semantics (as described above). 

Overall, I spent a tad over 9 hours working on the project this week. I spent 45 minutes critiquing
Andrew's project and a little over an hour formalizing my thoughts and design decisions in my notebook.
I spent the rest of the time working on the parser and semantics.

## Post-critique summary

Ellen critiqued my work last week. She thought that recurrences were pretty ambitious, largely because
the semantics of recurrences are not particularly clear or obvious in many cases. She also suggested
some ways of handling recurrences (such as basing future instances of a recurrence off of the current
instance). She also suggested using the `X <date>` syntax to denote completed tasks and raised a question
about the appropriate granularity for dependencies (does +1 day mean anytime the next day or 24 hours
later)?

## Post-critique reflection

I think Ellen raised some important points about recurrences, particularly that it's not immediately
clear which date is used to calculate the recurrence. By requiring a fixed recurrence interval (like
"every 2 weeks") and by preventing dependent tasks from having their own defined recurrences, I think
we have cleared up most of the semantic concerns; it should now be much clearer what is happening (even
though that clarity has come at the cost of a slightly smaller feature set).

I like the suggestion about completion syntax, but we've decided not to model task completion explicitly
in our syntax. Instead, completed tasks will be denoted in a separate "completed tasks" file (which is
maintained by the Sublime Text plugin). We initially arrived at this decision when we realized that marking
completion of a recurring task is rather difficult (and could quickly clutter up the task list). The approach
we've chosen directly models the approach taken by Gina Trapani's todo.txt (off of which our language is
roughly based).

I also think Ellen had some good ideas about the granularity of date arithmetic. For our current
implementation, we have decided to stick with the simple approach in which "+1 day" means "exactly
24 hours ahead." This is simpler to implement, and I think that it's slightly more clear. All dates in
our language are interpreted as points in time (rather than intervals). So, to "include" a whole day, a start
date would have to be at 12:00am and a due Date would have to be at 11:59pm. This would give "+1 day" two
distinct meanings, which could be a bit confusing. (That said, though, I think 12:00am and 11:59pm do
make sense as reasonable "default times" for the case in which a date is specified without an
accompanying time.)
