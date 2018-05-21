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

---

# What We <br>Forget To Test

<br>

<p>K. Adam White &bull; <a href="https://twitter.com/kadamwhite">@kadamwhite</a> &bull; Human Made</p>
<!-- .element: class="italic" -->

???

Thank you! Let's get started.

What is the hardest part of software development?

---

## Programming <br><small>is not the hard part</small>

???

It's not programming, I think. This may sound controversial, but think about it -- it's 2018 and we have the best languages, frameworks, and tools that have existed in the history of the web. It gets better every week.

---

### Team Communication
### Context Switching
### Project Handoff
### Documentation
### Code Review
### Bug Reports
### Onboarding

???

No, I think that the hard part of software development is what we do _just before_ and _right after_ programming. The actual coding is often the fun part; it's those tasks we have to complete before we start, or the things we need to do once we finish, that often feel the most difficult.

Whether you work for a product company, a consultancy, an agency, or for freelance clients, there's a lot of non-code tasks that are part of being a web developer.

In our sprint and project retrospectives we spend some time talking about what we could have done better technically, and a LOT of time discussing what we could do to improve these other processes. These are challenges we face on every project. Switching costs; Onboarding takes; the friction of team communication; code review; handoff.

---

### We're here to
## Solve Problems,
### not write code

???

We call ourselves programmers, but a programmer's job isn't really to write code. Our responsibility is to solve problems. The code is a means to an end; we should never forget that.

But all our tools are oriented towards code. I think it's a problem that we focus on that to the exclusion of these other parts of our day-to-day jobs.

---

## We test our code...
### How do we evaluate the rest?

???

I want to share some best practices we can use to evaluate and improve our processes; think of it as a style guide for everything that isn't code.

I don't have all the answers, and different teams require different processes. but we'll focus today on two important, complementary things: how we ramp up on a project, whether we're onboarding ourselves or helping our colleagues join the team; and how we improve communication within our teams to facilitate code review, task switching and handoff.

---

## Context Switching
### Humans Are Not Good At It

???

The hardest thing I've had to do as a developer recently is to admit that I'm bad at multitasking. I'm not good at context switching. Some folks are OK at it, but most of us think we're better than we are. Jumping between projects, especially projects with different organizational structures (such as a client project vs contributing to WordPress core), is just plain hard.

As I've admitted this to myself it has let me step back and compare the projects I work on, to figure out what helps me get going quickly and stay focused.

---

## The Onboarding Process

???

So let's talk about project onboarding. We want to be as productive as possible, but we lose so much time when we transition between tasks; how do you go from 0 to full speed on a new project?

(All of this excludes starting green-field projects; but some pieces are useful as rubriks when choosing you tools)

---

### Believe In The
## README

???

The best way is pair with another developer, but they may not have time. If we're on our own, whether we're ramping up on a client project, auditing an existing site, evaluating a new Composer or NPM package, or trying to contribute to an open source library on Github, the first thing we see is the README. This is what we view on NPM's package listing, this is the first thing we see on Github; the README is our entrypoint into the project.

---

(screenshot of https://github.com/wordpress/gutenberg)

???

The first thing I do whenever I join a project is to look through the README, and open issues for anything it doesn't explain. Because I think there's a very clear set of responsibilities that a README has, and if it doesn't meet them, it doesn't just slow _me_ down -- anybody hoping to contribute to or use the project may be held up. The running theme of this talk is going to be how to spend a little time up-front to save a lot later on, and the README is the most important part of this.

---

### What Is This For?
### How Do I Use It?
### How Do I Set It Up Locally?
### Where Is The Documentation?

???

A good README, in my opinion, should do a couple things:

- Tell you what a project is and is for, concisely and clearly
- Tell you in brief how use the project
- (Arguably most critically) explain how to get the project running locally for development
- Link to or provide more comprehensive documentation

---

## What Is This For
### (The Project Overview)

(https://github.com/reduxjs/redux#learn-redux)

The importance of a project overview should be obvious, but all too often neglected. Remember that this is the first thing that somebody will see when they view your project; keep it concise, but don't skip it!

This should include what environment your project is intended for; whether a JS library works in node or the browser, for example, or whether it's a WordPress plugin or a composer module.

---

How do you use this?

A lot of readme's don't include any setup or getting started steps; this is permissible if you link to a comprehensive documentation site, but I think it's great that even projects like Redux that DO have excellent documentation include a basic getting-started site right there in the README.

(https://github.com/reduxjs/redux "The Gist" example)

I take this a bit far on wpapi, and actually generate a good portion of the documentation by parsing and splitting up the README. This is probably overkill, but good documentation can make the difference between a good library that gets adopted and a great one that gets ignored, so it's worth the investment.

If you can practice documentation-driven development, do so!

Redux doesn't put _too_ much documentation in the README, but they actually go a lot further by including a really great list of tutorials, introductions and overviews. They include a variety of types of learning resource (video vs narrative blog posts vs technical documentation) to support many learning styles.

https://github.com/reduxjs/redux#learn-redux

They also have a helpful section that explains when Redux may NOT be the best solution for a project. Not many projects do this, and I really respect that they are clear about where the library should be used.

https://github.com/reduxjs/redux#before-proceeding-further

---

That's great for a package like Redux, but not all of that may seem useful for a plugin or theme. I would still expect that after reading your README, I could answer, "what would I use this plugin for," "how would I install it," and "how to I get it up and running on my site".

We're spoilt for choice in the WP ecosystem, so make it clear from the project's plugin directory landing page or Github readme why you'd want to use THIS plugin to solve your problems, instead of another. Be clear.

---

## Project Setup

One of the few things that's true for all projects is that we need to know how to set them up for local development.

(Either I am uniquely bad at getting a project running locally, or I'm uniquely good at finding gaps in the onboarding steps.)

For an npm package this may be as simple as running `npm install` or `yarn`, and some plugins may just need to be installed and activated.

But if you need to do any configuration or setup to use your theme, or need to seed your project with sample content, you should explain or link to a guide for those steps.

Be explicit with your dependencies.

If you provide a setup script, what do I need to run it? Will it only work on OSX, or can I run it successfully in Linux or Windows? What systems will I need access to?

Especially if you're releasing an open source project, do not assume that all your contributors will be using the same operating system!

---

For most WordPress projects, we use some sort of development environment -- many of them are built around Vagrant, like Chassis or VVV, but others use MAMP, XAMPP, Local by Flywheel, or Docker.

I like vagrant-based projects because they tends to reduce the cross-platform issues you might encounter with a team using for example a combination of MAMP and XAMPP; assuming you've got virtualbox and vagrant, you can work around most cross-platform problems by wrapping them in a provisioning script. However the barrier to entry is higher.










