# What We Forget To Test

## Abstract

Our project has 100% test coverage; we have end-to-end tests, unit tests, manual testing scripts—and my colleague can’t get any of it working!?

Poorly-written issues or out-of-date local installation steps can ruin a project, but when we think of testing we forget about the processes that surround our code. So how can we hold our workflows, onboarding steps and communication to the same rigorous standards of quality as our codebases? By applying that mentality to the issue trackers, READMEs and wikis we already have, we can save ourselves and our teams from communication and process errors and get back to making websites!

## Slides

---

# What We Forget To Test

K. Adam White &bull; @kadamwhite &bull; Human Made

---

Why do we build software?

(to solve problems for people)

---

Why do we test software?

To avoid repeating our mistakes

---

What do we test?

- How the application works
- That a bug has been fixed
- That business goals are met

We don't have tests for, is this easy to work on.

Debugging (murder mystery metaphore): https://twitter.com/fortes/status/399339918213652480?lang=en




"The title of the talk is of course what we forget to test, and you may have noticed that I didn't technically share any tests.

-----

THIS TIME FOR REAL YO

This talk, as with many others today, is the result of trying to come up with a solution to a hard problem.

With that in mind, the question I'd like to open with is,

What is the hardest part of software development?

I'm going to argue that it's not programming. This may sound controversial, but think about it -- it's 2018 and we have the best software tools, libraries and frameworks that have existed in the history of the web. And it's just getting better.

No, I think that the hard part of software development is what we do _just before_ and _right after_ we are programming. The actual coding is often the fun part, and it's those tasks we have to complete before we start, or the things we need to do once we finish, that often feel the most difficult.

To put this in context, many of us in this room work at agencies or take freelance contracts. The sort of difficulties I'm describing are the tasks we have to tackle every time we take on a new client, or switch between projects. Our switching costs; how long onboarding takes; the friction of team communication, code review, and handoff.

Our job as developers, after all, is not to write code. Our responsibility is to solve problems. The code is just a means to an end; we should never forget that. So I think it's a problem that we focus on the code to the exclusion of these other parts of our day-to-day jobs, and that concern is the genesis of this talk I want to share with you today.

So with that in mind, we're going to talk about two complementary things: how we ramp up on a project, whether we're onboarding ourselves or helping our colleagues join the team; and how we improve communication within our teams to facilitate code review, task switching and handoff.

---

Over the past two years the hardest thing I've had to do as a developer is to admit that I'm bad at multitasking. I'm bad at context switching. Some people are pretty good at it, but many of us think we're better than we are: Jumping between projects, especially projects with different organizational structures (such as a client project vs contributing to WordPress core), is just plain hard.

As I've admitted this to myself, it's let me step back and compare the projects I work on, to figure out what helps me get going quickly and stay focused. I'm going to walk through the process of onboarding to a new project, to share what I've learned by doing so.

(All of this excludes starting green-field projects; but some pieces are useful as rubriks when choosing you tools)

## Believe In The README / WRITE THE README

Whether we're ramping up on a client project, auditing an existing site, evaluating a new Composer or NPM package, or trying to contribute to an open source library on Github, the first thing we see is the README. This is what we view on NPM's package listing, this is the first thing we see on Github; these days the README is our entrypoint into the code.

The first thing I do whenever I join a project is to look through the README, and open issues for anything it doesn't explain. Because I think there's a very clear set of responsibilities that a README has, and if it doesn't meet them, it doesn't just slow _me_ down -- anybody hoping to contribute to or use the project may be held up. The running theme of this talk is going to be how to spend a little time up-front to save a lot later on, and the README is the most important part of this.

A good README, in my opinion, should

- Tell you what a project is and is for, concisely and clearly
- Tell you in brief how use the project
- (Arguably most critically) explain how to get the project running locally for development
- Link to or provide more comprehensive documentation







