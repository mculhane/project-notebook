# Design notebook for week ending November 9, 2014

## Description

This week, Christine and I decided to merge our project with Nick's. Together,
we will be creating a DSL for task management. We had originally planned to add
support for dates and dependencies to Gina Trapani's todo.txt. However, after
poking around in the source code for todo.txt for a while, we realized that we
would probably spend more time trying to integrate with todo.txt than it would
take for us to just generate the required functionality on our own. Furthermore,
todo.txt has a strict requirement that each task be contained in one line. While
we think that this is a noble concept for simple tasks, we wanted to allow our
language to include more detailed specifications of a task (such as start and
due dates/times, dependencies, and possibly notes). This would make a single
line per task unreasonable. So, the difficulty of extending todo.txt coupled
with the fact that we felt it necessary to deviate from one of todo.txt's core
philosophies helped us decide that we would create our own DSL from scratch.

In thinking about hwo a program in our language would run, we decided that the
syntax and IR could be powered via a variety of user interfaces. However, we
did want to have one interface built out for this project so that we could
demonstrate an actual use case (and end up with something that someone might
actually consider using). We decided that a Sublime Text plugin would be a
reasonable way to do this, as it would allow us to wrap additional functionality
around the syntax of our language.

We split up our work for the week as follows: Nick will work on an initial
attempt at the IR. Christine will work on an initial attempt at a syntax. I
will look into the feasiblity of a Sublime Text plugin. At our team meetings,
we will discuss our progress and shuffle tasks as appropriate.


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

**What questions do you have for your critique partners? How can they best help
you?**

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

* 1 hour
  * Team meeting, decided to work with todo.txt and create a Sublime plugin.
* 1 hour
  * Looked into feasibility of Sublime Text plugins and played around with a
    Hello World example.
* 1.25 hours
  * Team meeting, discussed IR/plugin/syntax in more detail. Thought about the
    semantics of due/start dates with recurrences and dependencies.


## Post-critique summary

## Post-critique reflection
