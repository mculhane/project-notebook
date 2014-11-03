# Design notebook for week ending November 2, 2014

## Description

This week we began the design process for our DSL. We had extensive discussion
regarding our domain and the particular subdomain that we intend to tackle
during this project. We formalized these thoughts in our DSL description.

We did a lot of brainstorming during this week's work, but the part I found
most effective was looking at other similar DSLs and how they tackle the
sorts of problems we're facing. In our work this week, we looked at two other
DSLs:
* [GNU Make](https://www.gnu.org/software/make/)
* [Todo.txt](http://todotxt.com/)

In addition to describing our DSL at a high level, we created a project
plan that outlines our schedule for the project and our goals regarding how
we will work together as a team. We'll do our best to stick to our plan, but
we'll constantly be revisiting it and tweaking it as we progress throughout
the semester.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

The most pressing issue for our project is probably the appropriate level of
specificity for the syntax. In particular, should the syntax explicitly declare
dependencies, or should task dependencies be inferred from other features of
the tasks/project? This issue is particularly pressing because it affects the
amount of computation that our language will need to perform and it will
directly inform our structure of an intermediate representation for our
language.

**What questions do you have for your critique partners? How can they best help
you?**

In addition to the "pressing issue" above, I'd be interested in how our critique
partners feel about the utility of our language. Do they feel
that a visual dependency graph is "sufficient" output for our language, or is
the output trivial given whatever effort is required to produce the input? Along
the same lines, is there any additional output that our critique partners feel
would seem useful? In other words, given our (yet-to-be-defined) syntax, what
would our critique partners imagine the output of a program to be?

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I didn't know we'd be asked this question, so I didn't make any effort to time
my work on the project this week. Thus, I can't give an exact answer, but I'd
estimate it to be at least a couple hours under the expected 9 hours for the week.
Christine and I did all work together/simultaneously this week (brainstorming
together and writing up responses simultaneously in Google Docs), so the labor
was shared incredibly equally.


## Post-critique summary

## Post-critique reflection
