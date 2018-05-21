**Abstract**

Our project has 100% test coverage; we have end-to-end tests, unit tests, manual testing scripts—and my colleague can’t get any of it working!?

Poorly-written issues or out-of-date local installation steps can ruin a project, but when we think of testing we forget about the processes that surround our code. So how can we hold our workflows, onboarding steps and communication to the same rigorous standards of quality as our codebases? By applying that mentality to the issue trackers, READMEs and wikis we already have, we can save ourselves and our teams from communication and process errors and get back to making websites!

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

The biggest context switch of all is to begin a new project.

How do you go from 0 to full speed on a brand new codebase?

The best way is pair with another developer, but they may not have time.

And while we can figure it out by reading the code, most of us can scan prose faster than PHP. So if we're on our own, the first thing we're going to look at is the README.

---

### Believe In The
## README

??? The README is a project's landing page and cover letter.

Because of this, I think there's a very clear set of responsibilities that a README has.

---

### What Is This For?
### How Do I Use It?
### How Do I Get Started?

???

A good README, in my opinion, should do a couple things:

- Tell you what a project is and is for, concisely and clearly
- Tell you in brief how use the project
- (Arguably most critically) explain how to get the project running locally for development
- Link to or provide more comprehensive documentation

The first thing I do whenever I join a project is to look through the README, and open issues to clarify or expand on anything of these that are missing.

---

## What Is This For?
### (The Project Overview)

(screenshot of https://github.com/wordpress/gutenberg#editing-focus)

???

It surprises me how often a README doesn't even attempt to explain what a project does, especially for NPM modules.

Remember that this is the first thing that somebody will see when they view your project; keep it concise, but don't skip it!

This should include what environment your project is intended for; whether a JS library works in node or the browser, for example, or whether it's a WordPress plugin or a composer module.

---

## How Do You Use It?
### (The Documentation)

(https://github.com/reduxjs/redux#learn-redux)

???

So now I know what this is for. How do I install it? How do I use it in my project?

For small projects such as webpack plugins the README is often the entity of the documentation, and that's just fine. I take this a bit far on my wpapi library, and actually generate most of the documentation website by parsing content from the README.

You can link to a docs site, but I think it's great that projects like Redux that DO have excellent documentation still include a basic getting-started site right there in the README.

---

## How Do You Use It?
### (The Documentation)

(https://github.com/reduxjs/redux#before-proceeding-further)

??? 

They also have a helpful section that explains when Redux may NOT be the best solution for a project. Not many projects do this, and I really respect that they are clear about where the library should be used.



---

## How Do You Use It?
### (The Documentation)

https://github.com/humanmade/WordPress-Importer#how-do-i-use-it

???

For a WordPress plugin, this section may look like a quick overview of features

After reading your README, I should answer, "what would I use this plugin for," "how would I install it," and "how to I get it up and running on my site".

We're spoilt for choice in the WP ecosystem, so make it clear right from Github or the plugin directory landing page why you'd want to use THIS plugin to solve your problems. Be clear.

---

## Documentation-Driven Development?

???

As an aside, we often ask how to keep our documentation up to date. Maybe we can think of it like TDD: After we write our tests describing the technical behavior of the code, we can write the documentation explaining the human interface. Then we write the code that satisfies both.

---

## Documentation:
### Support Different Learning Styles

(https://github.com/reduxjs/redux "The Gist" example)

???

As an example, Redux doesn't put _too_ much documentation in the README, but they actually go a lot further by including a really great list of tutorials, introductions and overviews. They include a variety of types of learning resource (video vs narrative blog posts vs technical documentation) to support many learning styles.

https://github.com/reduxjs/redux#learn-redux

---

## How Do I Get Started?
### Project Setup

???

We're moving out of README territory into CONTRIBUTING.md, now; for any project, we'll need to know how to set it up for local development.

For an npm package this may be as simple as running `npm install` or `yarn`, and some plugins may just need to be installed and activated.

But if you need to do any configuration or setup to use your theme, or need to seed your project with sample content, you should explain or link to a guide for those steps.

---

## Project Setup
### Explicitly Define Dependencies

???

Be explicit with your dependencies.

If you provide a setup script, what do I need to run it? What systems or servers do I need access to? Do I need NPM or Composer?

Will it only work on macOS, or can I run it successfully on Linux or Windows? Especially if you're releasing an open source project, do not shut out contributors coming from other operating systems!

---

## Project Setup
### Use Established Tools

???

We've got a lot of WP dev environments available -- many of them are built around Vagrant, like Chassis or VVV, but others like Local by Flywheel use Docker, and of course MAMP & XAMPP are going strong.

It's tempting to assume that other developers will use the same tools you do, but unless you specify consistent tools people tend to do their own thing.

This is why Vagrant is great, it can standardize the way your project runs across OSs.

But even with Vagrant, it's better to leverage existing setup scripts like WP-CLI than to invent your own. You want to get going so you can debug your application code, not get hung up debugging your virtual machine!

---

## Project Setup
### How Do I Get Sample Data?

???

And the piece that is _always_ skipped: how do I populate my VM database with sample data to get this running? It's a lot easier to see how something works if there's data locally, so make this as easy as possible.

If you're taking backups from production, don't forget to scrub out any anonymous data first!

---

## Project Setup
### Keep It Up To Date

???

The best way to make sure your installation instructions are current is to have somebody join the project. Things will break unexpectedly. This always happens to me; Either I am uniquely bad at getting a project running locally, or I'm uniquely good at finding gaps in the onboarding steps!

when they do, pair the newcomer with an existing dev to work through them, and update the documentation accordingly.

You can replicate this on your own by deleting and recreating your dev environment every sprint. Most teams won't go this far, but if you can bring yourself to do it, you'll be forced to keep things up to date for your own peace of mind.

---

## Project Setup
### Put Your Setup Steps In Version Control

???

The setup process is tightly coupled to your code so it can be valuable to version it along with the rest.

However, a wiki's the best choice if you need to coordinate multiple repositories.

---

## You're up and running!

???

Great! You're up and running. 

---

# Issue & Pull Request Templates

???

One of my favorite features of Github is their issue and PR templates.

---

## `.github/PULL_REQUEST_TEMPLATE.md`
