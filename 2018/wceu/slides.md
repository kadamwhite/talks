# <small>What We</small> Forget To Test

<br>

<p>K. Adam White &bull; <a href="https://twitter.com/kadamwhite">@kadamwhite</a> &bull; <img src="./images/hm-logo.png" style="height:1.5em;margin:0 0 -0.4em;display:inline-block" alt="Human Made Logo"/></p>
<!-- .element: class="italic" -->

???

Thank you!

---

_Rejected Alternative Titles:_

### Write Your Process Down

### How To Raise Your Markdown Files

### Docs-Driven Development

### README (Or Else)

???

This talk has evolved somewhat since I proposed it, and I've gone through a lot of titles that would have been better than what's in the program.

But in short, I'm here to argue that we spend too much time talking about code. 

---

## Programming <small>Is Not The Hard Part</small>

???

Code's fun, but it's not the hard part of what we do. It's hard, sure! But we have the best tools we've ever had in the history of the web. No, coding gets easier every week.

---

### Team Communication
### Context Switching
### Project Handoff
### Documentation
### Code Review
### Bug Reports
### Onboarding

???

The hard part's everything we do _between_ the small periods when we're writing code. We face these other challenges on every project.

We've got good tools for evaluating our code, but there's no unit tests for team communication; no linting for pull request discussions or onboarding instructions.

Fortunately, we CAN evaluate the documentation we leave ourselves to help with these processes. And that's what I'm going to talk about today.

---
<!-- .slide: data-background="images/example-bad-pr.png" data-background-position="center top" -->

## <small>What Makes A</small> Good PR?
<!-- .element: class="align-right blackoutline" -->

???

This talk occurred to me when I was asked to review a bad PR.

What made it bad? The code was actually fine. I'm glad it's tested, and that it passes lint. But I could have answered both questions by looking at the code and CI results; what's written here is useful only to the developer opening the PR.

Without any description, it doesn't tell me what's being addressed.

It doesn't tell me what to test or how to test it.

---

### A &ldquo;Good&rdquo; PR Description should

- Summarize the issue being addressed
- Link to the acceptance criteria or requirements
- Contain screenshots of before/after changes, or gifs showing interaction
- Explain any unusual design decisions
- List specific testing instructions as needed

???

We can suss much of this out from the code, but we're all faster at reading prose. Leaving them information is not just kind, it's critical to good team communication. Leaving things out just introduces back and forth, which can take days across time zones.

Fleshing out PR's this much may feel like it's a waste of your time, but you're asking your colleagues to do the harder part: to stop what they are doing, and try to understand your code.

---

## Context Switching <small>Humans Are Not Good At It</small>

_Leave instructions to help your team pick up where you left off!_
<!-- .element: class="fragment" -->

???

If you're doing code review, you're stepping into somebody else's thought process. It's a context switch.

Context switching and multitasking are things we as humans are not good at. I myself am extremely bad at multi-tasking. I get really distracted when I try to switch tasks.

(advance!) Take an extra five minutes when you're opening a PR to give your teammates as much help as possible, and it'll be easier for them to dig in quickly. That means switching takes less time, and we can get back to coding faster.

---
<!-- .slide: data-background="images/gutenberg-pr-template.png" data-background-position="center bottom" -->

???

How do we ensure we actually do this? We leave ourselves instructions, right in the PR description window.

We can use GitHub's PR templates to document our process and remind us of the communication quality standards that we have for ourselves and our teammates.

By putting markdown files in a `.github` folder at the top of our project, we can control what our collaborators see when we open pull requests or issues, and include project-specific instructions.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-issue-template.png" -->

???

This is Gutenberg's issue template, which reminds bug reporters to include what they expected to happen, specifics about what went wrong, and steps to reproduce a bug.

Issue and pull request templates also let you use HTML comments which are hidden in the final output, but which help ensure that the ticket is thorough.

---

## Don't Make Your Colleagues Guess

_(It will help you, too)_

???

Without templates we often get vague issues, because even with best of intentions we're usually in a hurry and don't want to take the time to go into detail.

But if I write a vague issue and come back to it after three sprints or so, I'm toast. Where do I start? I have to reassemble everything I knew about the problem before I can get back to where I was when I opened the ticket. Why not just write it down in the first place?

I'm a firm believer in putting as much detail and supporting material into tickets as possible. Putting in the time to write a good issue leaves me an on-ramp I can use to get back up to speed.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-pr-template-detail.png" -->

???

_Especially_ with open source projects, more detail is better. Your potential collaborators won't know how best to help you unless you tell them. And look at projects like Gutenberg — it works!

---

### Write Your Process Down

???

These templates don't mean you have to fill out every section for every ticket.

They're just a reminder to respect our colleagues' time as we would our own, by being specific and direct. They let us hold our team process to a common standard.

Although we're bad at context switching, we're often not bad at following instructions. Instructions mean documentation. Writing things down saves time and improves communication.

---


Jumping between tasks or projects, especially tasks that require different types of thinking or communication, is just plain hard. Some folks are OK at it, but almost all of us think we're better than we are.

The hardest thing I've had to do as a developer recently is to admit once and for all that I'm bad at context switching. I can't multitask. 

As I've admitted this to myself it has let me step back and compare the projects I work on, to figure out what helps me get going quickly and stay focused.

---

???

The small pieces of documentation we leave ourselves in our repositories play an important role in easing the transitions between tasks, and keeping us focused on the project.

---

### Believe in
## Written Documentation

???

I work on a distributed team; if I need to set up my local dev environment or fix a bug, I can't go over and ask a colleague how to pull down sample data or how a feature is supposed to work.

We can puzzle out answers from the code, but that takes far too much time. I need that information to be _written down_ and embedded in the project I'm working on, so that I can quickly answer those questions for myself.

---

### Believe In
## Markdown Files

_Co-Locate Your Documentation_

???

I like comprehensive documentation sites, but I like the markdown files in our repositories even more. To quote my colleague Joe McGill, if you need to let people know what they need to know, the best way is to write it down as close to the thing they're going to interact with as possible.

The markdown files in our repositories are co-located documentation. So long as I have the code checked out, I also have the instructions! These can be fleshed out in design documents or the project wiki, but the markdown files are accessible in a way these other resources are not.

---

### README.md
### CONTRIBUTING.md
### .github/ISSUE_TEMPLATE.md
### .github/PULL_REQUEST_TEMPLATE.md

???

I'm going to focus on the markdown files that GitHub supports natively, but even if you use another VCS or issue tracker these tasks can be replicated with your own tool suite.

So how do we best use each of these files?

---

# README.md

### What Is This For?
### How Do I Use It?
### How Do I Get Started?

??? The README is a project's landing page and cover letter.

It has a few key responsibilities — a good readme should, in my opinion,

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

## How Do I Get Started?
### Project Setup

???

We're moving out of README territory into CONTRIBUTING.md, now; for any project, we'll need to know how to set it up for local development.

For an npm package this may be as simple as running `npm install` or `yarn`, and some plugins may just need to be installed and activated.

But if you need to do any configuration or setup to use your theme, or need to seed your project with sample content, you should explain or link to a guide for those steps.

---

### Project Setup
## Explicitly Define Dependencies

???

Be explicit with your dependencies.

If you provide a setup script, what do I need to run it? What systems or servers do I need access to? Do I need NPM or Composer?

Will it only work on macOS, or can I run it successfully on Linux or Windows? Especially if you're releasing an open source project, do not shut out contributors coming from other operating systems!

---

### Project Setup
## Use Established Tools

???

We've got a lot of WP dev environments available -- many of them are built around Vagrant, like Chassis or VVV, but others like Local by Flywheel use Docker, and of course MAMP & XAMPP are going strong.

It's tempting to assume that other developers will use the same tools you do, but unless you specify consistent tools people tend to do their own thing.

This is why Vagrant is great, it can standardize the way your project runs across OSs.

But even with Vagrant, it's better to leverage existing setup scripts like WP-CLI than to invent your own. You want to get going so you can debug your application code, not get hung up debugging your virtual machine!

---

### Project Setup
## How Do I Get Sample Data?

???

And the piece that is _always_ skipped: how do I populate my VM database with sample data to get this running? It's a lot easier to see how something works if there's data locally, so make this as easy as possible.

If you're taking backups from production, don't forget to scrub out any anonymous data first!

---

### Project Setup
## Keep It Up To Date

???

The best way to make sure your installation instructions are current is to have somebody join the project. Things will break unexpectedly. This always happens to me; Either I am uniquely bad at getting a project running locally, or I'm uniquely good at finding gaps in the onboarding steps!

when they do, pair the newcomer with an existing dev to work through them, and update the documentation accordingly.

You can replicate this on your own by deleting and recreating your dev environment every sprint. Most teams won't go this far, but if you can bring yourself to do it, you'll be forced to keep things up to date for your own peace of mind.

---

### Project Setup
## Put Your Setup Steps In Version Control

???

The setup process is tightly coupled to your code so it can be valuable to version it along with the rest.

However, a wiki's the best choice if you need to coordinate multiple repositories.

---

### You can use more than one README!

???

You can also have more than one README in your codebase! If you view a folder in GitHub and that folder contains a README, github will display that readme. This is a great place to put more extensive design documentation or feature overviews that only apply to part of the codebase.

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

---

# Issue & Pull Request Templates

???

One of my favorite features of Github is their issue and PR templates.

---

## `.github/PULL_REQUEST_TEMPLATE.md`

