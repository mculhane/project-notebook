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

I think the most pressing issue for our project is the intermediate
representation, mostly because it directly impacts both the syntax and the
semantics (which could otherwise be developed separately). In particular,
we are spending a lot of time thinking about how we could model both
recurrences and dependencies (and, as more of a challenge, dependencies
between recurring tasks). This question will directly inform how we
structure tasks and the sorts of data structures we use to model them, so it
is imperative that we get a (hopefully good) solution soon.

**What questions do you have for your critique partners? How can they best help
you?**

Because I focused on the Sublime component of our project this week, I'll focus
my questions on that topic.

Does a Sublime plugin make sense and/or sound useful as a way of managing tasks?
(Clearly, a Sublime plugin would limit our target audience to people who
actually use a text editor like Sublime Text.) Also, what level of detail would
make sense for a Sublime plugin?

Should a Sublime Text plugin look like set of tools and syntax to
improve the experience of natively writing in our language, or should it
provide a more sophisticated interface that hides the underlying language and
instead only uses it as a database for loading/storing tasks? There are pros
and cons to the two approaches. The first highlights and showcases our language,
while the second introduces a more robust and complete user experience. We may
need/want a combination of these approaches, perhaps writing natively in our
DSL to create/modify tasks, but then also providing useful aggregations of that
data (such as tasks due in the next 2 days or tasks that are not "blocked" by
dependencies or future start dates).

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

The times listed below do _not_ include time spent working on the project in class.

* 1.5 hours
  * Critique of Philip's project (and learning a _lot_ about flavors of Markdown).
* 1 hour
  * Team meeting, decided to work with todo.txt and create a Sublime plugin.
* 1 hour
  * Looked into feasibility of Sublime Text plugins and played around with a
    Hello World example.
* 1.25 hours
  * Team meeting, discussed IR/plugin/syntax in more detail. Thought about the
    semantics of due/start dates with recurrences and dependencies.
* 2 hours
  * Played around more with Sublime Text plugins and focused on how they
    can create/modify settings and menu items.
* 0.75 hours
  * Worked on project notebook and created critique summary.
* 1.5 hours
  * Spent a while looking at Scala vs. Python as a suitable host language. A summary of conclusions/musings is [here](https://github.com/mculhane/project/wiki/Host-Language-Thoughts).


## Post-critique summary

Note: This is a summary of Nick's critique of our original language, which was
a language for modeling dependencies. Our project has since merged with his and
changed focus quite a bit.

Nick's critique focused on a few things. He mentioned that the majority of the
work likely lies in the language design. He also mentioned that it may be wise
to build on top of todo.txt. Nick also hit on a very important point about
dependencies, which is that it's absolutely imperative to strike a balance
between something so simple that it's not useful and something so complicated
that the upfront effort outweighs any benefits that the language provides.

## Post-critique reflection

We have changed our project's focus substantially since the critique, so much of
Nick's initial critique is less relevant. However, there are definitely some
important points we can learn from.

First, Nick's comments about striking a balance between simplicity and utility is
still very important, and it's something we'll have to keep in mind. Even if we
can build a ton of cool functionality around very detailed and parameterized tasks,
those features will not be useful if the time they save is less than the time
invested in setting up the tasks.

Next, Nick commented/suggested that the majority of the project focus on the
language design (syntax and IR). I think this is still a useful point to consider.
The biggest challenges of our project seem to be in coming up with a clear and
logical way to represent dependencies, recurrences, and their interactions, so it
makes sense that we would focus on that space. That said, though, we are a team
of 3, so it would probably make sense for us to accomplish more than a smaller
team of one or two people. Thus, I think it is still reasonable to have a goal
of developing a more polished end-to-end system that someone could actually use
for their personal task management. (I'm sure we'll clarify/adjust the exact scope
of the project during conversations with Prof. Ben in the coming week or so.)

Nick's point about focusing on todo.txt is one that we've decided to forgo, but
not without much discussion and consideration. (See my comments on this in the
project description section above.)
