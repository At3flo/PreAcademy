# By Tomorrow?! Time and project management

* [Goal of this unit](#goal-of-this-unit)
* [Laws of time](#laws-of-time)
* [The two mistakes](#the-two-mistakes)
* [List all the required tasks](#list-all-the-required-tasks)
* [Assign time to each task](#assign-time-to-each-task)
* [Busy is the new stupid](#busy-is-the-new-stupid)
* [Parallel vs Serial development](#parallel-vs-serial-development)
* [Re-scheduling](#re-scheduling)
* [Spiral development. Failing as fast as you can](#spiral-development-failing-as-fast-as-you-can)
* [Debugging. When things go wrong](#debugging-when-things-go-wrong)
* [Deliver](#deliver)
* [Using Gitlab/Github to manage your projects](#using-gitlabgithub-to-manage-your-projects)

## Goal of this unit

The goal of this unit is learning some **techniques** to become more **efficient** managing your **time** and projects.

## Laws of time

Time has three peculiarities, which I elevated to laws.

* **First** law of time. **Everything consumes time**
* **Second** law of time. **You can't stop time**. There is nothing you can do about it. You can pause but time will not
* **Third** law of time. **Time x Effort = constant**. Given an initial large time to do something, the effort will be low. As time tends to zero, the effort tends to infinite.

## The two mistakes

There are **two mistakes** people make when **managing time**. The **first one** is thinking about it as a continuous, **infinite** line, whose duration is **relative**. Do this and you will always be late. You need to start thinking about time as a physical dimension like length, finite and perfectly measurable.

The **second mistake is overestimating time**. We tend to think, given a deadline, that we have plenty of time to finish a task. This is a big mistake. Let's break down a one week deadline, for example.

**Consider that a week has 5 days**, not 7. Some people affirm they will work 7 days. They fail miserably.

In theory, you will have 8 hours available everyday for working/studying, often splitted between the morning and the afternoon. But that time will be reduced because of the 3 reasons below.

* Assume that **an hour is 50 minutes**
* Assume **you will spend 1 hour every morning/afternoon in emails**, calls, messages, **and the like**. If not more
* Assume that **you will take a 30 minutes break** at mid morning/afternoon

So in reality you have roughly 5h. That is assuming that you are not a social network addict. To recap, **in a week you have less than 24h of continuous work**.

> **Learn by doing:** Make a calendar of available time for working in a project.

## List all the required tasks

The idea behind project management is simple: To allocate every task in our project in a bidimensional matrix of time (days as columns, hours as rows). We only have two uncertains: **The first uncertain is knowing how many pieces (tasks) we have in the puzzle**. The second uncertain is how long it will take to complete each task. Sometimes you will forget the first law of time and you will not consider a task, because you think it won't consume a noticeable amount of time. Here are a list of commonly ignored tasks that make your project fail:

* Determining the project management strategy. It consumes time.
* Researching. It consumes time.
* Lab cleanup. It consumes time.
* Documenting. It consumes time.
* Multimedia processing. It consumes time.
* Testing. It consumes time.
* Unforeseen. They exist and consume time. Allocate time for it.
* Troubleshooting and debugging (no, this is not an unforeseen, this is a mathematical certain). It consumes time.
* Rehearsing a presentation. It consumes time.

> **Learn by doing:** List all your required tasks and assign them a priority.

## Assign time to each task

In project management there are two variants of how much time you spend on a task. One is called **demand-side**, in which you start a task and wait until it is completed to continue. If you had infinite time, you could proceed this way. But you haven't. One of the best things of fab academy is the one week cycle. That time is not enough to complete the task in demand-side mode, so it forces you to exercise your project management skills.

Some tasks though, are out of your control. There is nothing you can do about it. *It takes nine months to make a baby, no matter how many people you put on the job* is a popular American business proverb.

For things that are under your control -like designing a circuit, or researching for inflatable structures- you don't keep going until you finish. Because you will never finish. Instead, you will use the **supply-side** time management, in which you decide beforehand how much time are you going to spend on a task. You do the best you can in that time, and then you stop and switch to the next task. You have to estimate the time (according to your skills) and stick to it. Over time you will become more realistic in your supply-time estimations.

Work backwards from the deadline and forward from current time, iterating until you find a match.

> **Learn by doing:** Assign time to all your tasks.

## Busy is the new stupid

Don't be this person:

![busy](img/pm/busy.jpg)

Make sure that you don't fill up your calendar with tasks, leaving no time for you to sit back, have some headspace and do some critical thinking.

## Parallel vs Serial development

It is important to analize which tasks are independent, so that you can execute them in parallel and which tasks are dependent and you have to wait to start them. Always **throw as many parallel processes as your sanity can handle**. In particular, the **documenting** process should be **always running in parallel**.

> **Learn by doing:** Divide your taks in parallel and serial. Find out how much you can do at the same time.

## Re-scheduling

If you **overestimated time** or **ignored the third law** of time you will probably need to reschedule. It will also be the time to **drop some unrealistic goals** you had in mind. Remember that the most important thing is to deliver.

## Spiral development. Failing as fast as you can

If you try to create the project you have in your mind in one go, you will fail. Nature never achieves perfection in one attempt, but in a series of infinite iterations. At least, you have to reach the following milestone iterations:

1. Make it work. There is a fundamental design principle called *satisfizing* and here it is summarized: Doesn't matter how, but it has to work. ![](./img/pm/itruns.jpg)
2. Make it integrated and resilient. At the very minimum, make it holdable in one hand and resistant to shakes
3. Make it nice

Refine your project over and over until

1. You are happy with the result
2. You run out of time

> **Learn by doing:** Plan some iterations for your final project.


## Debugging. When things go wrong

Imagine you made a circuit board and it doesn't work. Somehow, you find there is problem in the design.

> **Learn by doing:** What do you do?

Things will go wrong, the only thing you don't know is by how much. The previous example was about a circuit board. But it could apply for anything else. You have two things to do.

1. **Top-down debbuging**: Franken-Fix the board. Do not make a new board. The goal is learning, not succeeding. Even if you found the problem in the design, no one said that this was the only flaw. Worse is the case if you make a new board and succeed, like the donkey and the flute kid's fable.
2. **Bottom-up debugging**: Find the root cause that originated the flaw. Sometimes the root cause is hidden behind intermediate causes. Ask yourself *why did that happen?* a few times until you find the root cause.

> **Free tip:** When debugging, always smile. Tomorrow, it will be worse.

## Deliver

The only thing certain in project management is that **there is a deadline**. At that day you **have** to deliver. Doesn't matter if it is not what you wanted, if you don't like it, or if you are halfway done. That day, you deliver whatever you have. Afterwards, if you want, you can meditate about what changes you should make in the future to achieve your goals. But remember, you deliver that ugly thing you made. Always. **Deliver**.

## Using Gitlab/Github to manage your projects

Among the many tools you can use for project management there is one special mention: gitlab/github. They have incorporated project management through *issues*. To keep it simple, you should open as many issues as tasks you must finish.

> **Learn by doing:** Using what you have learned, create a few issues of tasks you must do to complete an assignment.

![gitlab](img/pm/pm1.png)

To keep track of what has been done, you create **boards** that you name according to the status of the issues: `TODO`, `doing` and `done` are common name for boards, but you can create your own. Managing a project this way is very intuitive. You simply drag the issue card from one board to another to change its status. Issues placed in the `done` board are automatically closed.

![boards](img/pm/board.png)

> **Learn by doing:** Create some boards and add some tasks (issues) to the `TODO` or `doing` boards.

You can also use **tags** to classify the issues in categories like `bug`, `enhancement`, `electronics`, etc. If you were part of a team you can also **assign** the taks to other team members.

> **Learn by doing:** Create and assign some tags to your issues. Remember, an issue can have more than one tag.

Managing projects in gitlab is very **convenient**. It doesn't have all the bells and whistles of other project management tools. But you are **tracking everything in the same environment**, which has an extra value.

---
[Back to Summary](../summary.md)
