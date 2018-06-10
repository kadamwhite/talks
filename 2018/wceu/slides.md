# <small>What We</small> Forget To Test

<br>

<p>K. Adam White &bull; <a href="https://twitter.com/kadamwhite">@kadamwhite</a> &bull; <img src="./images/hm-logo.png" style="height:1.5em;margin:0 0 -0.4em;display:inline-block" alt="Human Made Logo"/></p>
<!-- .element: class="italic" -->

???

Thank you!

OK. "What we forget to test."

---

# <small>In Defence of the</small> README

???

Last month I was talking to a developer who maintained a large number of interconnected applications, and I asked what they did for documentation. They replied, "just README files," sounding almost embarrassed.

I'm here today to argue that the humble markdown files in our repositories are under-appreciated, and that we can improve our projects and our team communication by giving them the respect they deserve.

---

### Team Communication
### Context Switching
### Project Handoff
### Documentation
### Code Review
### Bug Reports
### Onboarding

???

Programming isn't the hard part of what we do. No, the hard part's everything we do _in between_ the small periods when we're writing code. These other challenges we face on every project.

We can't rely on unit tests or linting to ensure these tasks go smoothly. The best tool we have is our documentation.

---
<!-- .slide: data-background="images/example-bad-pr.png" data-background-position="center top" -->

## <small>What Makes A</small> Good PR?
<!-- .element: class="align-right blackoutline" -->

???

We think of documentation as a record of what our code does or how to use our applications, but we can also document process. By doing so, we can see where our process is failing.

As an example, take this pull request. There's no description explaining what's being changed, or how I should test it.

If I'm asked to review this code, the best I can do is skim it for obvious logical errors; I can't say whether I think it's a good solution to a problem, because I don't know the problem it solves.

---

## Context Switching <small>Humans Are Not Good At It</small>

_Leave instructions to help your team pick up where you left off!_

???

If you're doing code review, you're stepping into somebody else's thought process. It's a context switch.

Context switching and multitasking are things we as humans are not good at.

When you take an extra five minutes when opening a PR to give your teammates some background, it's easier for them to dig in quickly.

---

### A &ldquo;Good&rdquo; PR Description should

- Summarize the issue being addressed
- Link to the acceptance criteria or requirements
- Contain screenshots of before/after changes, or gifs showing interaction
- Explain any unusual design decisions
- List specific testing instructions as needed

???

A thorough written explanation, with screenshots or gifs of screen recordings where appropriate, gives me the context I need to do a thorough review.

Leaving these things out introduces back and forth, which can take days in a team distributed across time zones. Better team communication saves everybody time.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-pr-template-detail.png" -->

???

How do we ensure we actually do this? Documentation.

GitHub supports creating markdown file templates that control what we see when we open pull requests or issues.

These template files can include HTML comments that are hidden in the final output, but that convey instructions to help ensure the ticket or PR description is thorough.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-issue-template.png" -->

???

Gutenberg's issue template, for example, reminds bug reporters to include

- what they expected to happen,
- specifics about what went wrong, and
- steps to reproduce a bug.

I try to put as much detail and supporting information into my tickets as possible. That leaves me a great on-ramp I can use to get back up to speed when I return to the bug later.

---

## Don't Make Your Colleagues Guess

_(It will help you, too)_

???

Without templates we often get vague issues, because even with best of intentions we're usually in a hurry and don't want to take the time to go into detail.

_Especially_ with open source projects, more detail is better. Your potential collaborators won't know how best to help you unless you tell them what you need to know.

---

### Write Your Process Down

_Issue & PR templates define your team's  
communication quality standards_

???

Documented process makes a healthy team. Writing things down doesn't mean you lose flexibility -- not every template section is relevant for every ticket, and that's OK.

What it DOES is reduce ambiguity.

Documented processes remind us to respect our colleagues' time as we would our own, by being specific and direct. They let us hold our team processes to a common standard.

---

## Colocated Documentation

_Keep documentation close to the task or code it documents_

???

These templates have a visible impact on team behavior because they're _right there_ when you open a PR or issue. They work because they're inescapable.

The proximity of the _documentation_ to the _task_ is important. You may know the saying, "out of sight, out of mind" -- if it takes too long to look up how to do something, that documentation is worthless.

This is why I'm such a fan of markdown files, because they fit into our existing repositories right alongside our code.

---

# README.md

- What Is This For?
- How Do You Use It?
- How Can I Run It Locally?
- Where Are The Docs?

???

The humble README is a great example. This is an incredibly important document within your repository. A README is your project's landing page and cover letter.

A good readme has the responsibility to

- Tell you what a project is and is for, concisely and clearly;
- Tell you in brief how use the project;
- Provide or link to directions for running the project locally; and
- Provide or link to more comprehensive documentation.

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme.png" -->

### What Is This For?
<!-- .element: class="align-right blackoutline" -->

???

I like README's like Redux's, which contain everything but the kitchen sink: not just a brief blurb on what Redux is and why you should use it,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-philosophy.png" -->

### Project Philosophy
<!-- .element: class="align-right blackoutline" -->

???

but also a philosophy statement,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-the-gist.png" -->

### Usage Overview, <br>Learning Resources & Comprehensive Docs
<!-- .element: class="align-right blackoutline" -->

???

a "the gist" quick-start guide,

links to comprehensive documentation and a _copious_ set of examples and tutorials, including blog posts, video guides, and sample apps,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-before-proceeding.png" -->

### When Should I <br> _Not_ Use This?
<!-- .element: class="align-right blackoutline" -->

???

and (my favorite), a prominant section about when Redux might NOT be the best choice for a project!

---

## Tailor To The Task

???

That's obviously a lot of different types of content, but it's appropriate to a project like Redux that defines an architectural pattern you'd be using throughout your codebase. A JS module will require different types of documentation than a feature plugin or a client site.

---
<!-- .slide: data-background-position="center top" data-background="images/hm-website-setup.png" -->

???

The READMEs for our projects at Human Made will focus on defining team roles & responsibilities and how to set up the project for local development. It's the first point of entry if we need to hand the project off within our company, or onboard a new contributor from a client's team.

Within Human Made we actually have a README generator tool to ensure a new client project kicks off with all the baseline documentation already in place.

---
<!-- .slide: data-background-video="images/gutenberg-readme-overview.webm" -->

???

Gutenberg's readme, by contrast, emphasizes the project's goals, philosophy and roadmap. These make for an equally good introduction, given the different intent of the project.

The README doesn't have to do everything: setup and development workflow steps are shifted into some specific other files.

---

## CONTRIBUTING.md: <small>What Do I Need To Know?</small>

- Code of Conduct
- Community & Behavioural Expectactions
- Development Dependencies
- Workflows & Guidelines
- Chain of Command
- Release Process

???

One of these is CONTRIBUTING.md, a standard file name where you can put everything that a developer will need in order to dive into the project.

This includes technical information like local development environment setup instructions, but also information about project management, team roles and leadership hierarchies, workflows, and behavioral expectations.

---
<!-- .slide: data-background-position="right center" data-background="images/gutenberg-contributing-callout.png" -->

???

CONTRIBUTING.md can be supplemented with a CODE_OF_CONDUCT.md, and if either is present in your repository then GitHub will direct people to it when they open an issue or a PR.

Just like with issue templates, this puts a link to the documentation right where it will be of most use to the person who needs it -- GitHub does a great job with this, in my opinion.

---

### Encourage Contributions!
<!-- .element: class="align-center" -->

> <small>Thank you for thinking about contributing to WordPress' Gutenberg project! If you're unsure of anything, know that you're <strong>100%</strong> welcome to submit an issue or pull request on any topic. The worst that can happen is that you'll be politely directed to the best location to ask your question, or to change something in your pull request. We appreciate any sort of contribution, and don't want a wall of rules to get in the way of that.</small>

???

I think one nice thing the Gutenberg team does here is that they open their CONTRIBUTING file with a welcoming message that encourages participation. It's important to remember that contributing to open source can feel really hard or intimidating, so do what you can to make people feel comfortable asking questions.

And please, please be nice when you close off-topic issues!

---

## Local Markdown Documentation

???

All of these files we've discussed are project-level, but we're not limited to just those files for which GitHub has special handling.

The WordPress REST API, Redux, Gutenberg, all of these projects don't just use markdown files for repository workflow guides; the user-facing documentation content itself is authored as markdown files, often right there in the same repository alongside the code.

---
<!-- .slide: data-background-position="left top" data-background="images/readme-files-in-gberg.png" -->

???

In a modular project, you can also scatter READMEs and other files throughout your repository tree to explain how each module works!

This is something else that Gutenberg does to good effect.

When nested within individual module folders in your codebase not only will the README text be picked up when you browse to that folder in Github, but it can also be integrated in tools like React Styleguidist and Storybook.

---

## Documentation-Driven Development
<!-- .element: style="font-size:2.8em" -->

???

If your docs are kept next to your code in the same repository, you can easily update the docs when you update the code — or you can go even further, and write the docs firtrst.

My fellow core contributor and colleague at Human Made Joe McGill has described how he has seen features begin as a text file in an empty directory. 

That file contains architectural notes on the challenges and how the team expects to approach them, and it lives as part of the project while they write the code around it.

In the end, that markdown file becomes the readme for the new functionality.

---

## <small>You Don't Need To Use</small> Markdown Files

Wikis can be OK, too! Just write things down _somewhere_.

???

Nothing we've discussed today is GitHub specific or Markdown specific.

If you want to encourage contribution from team members without write access or if you need to coordinate one set of docs across multiple repositories, a wiki may be a better choice.

Or you can write your docs in a CMS, like we do with the WordPress handbooks -- although I will note the Gutenberg and REST API handbooks are now sync'd from Markdown files, which makes managing contributions easier IMO.

---

## Take The Time <small style="font-style: italic;">to write things down</small>
<!-- .element: class="align-center" -->

## Take The Time <small style="font-style: italic;">to keep docs updated</small>
<!-- .element: class="align-center" -->

???

Documentation doesn't happen unless you make time for it. What we've discussed today is the tip of the iceberg of the benefits of writing and maintaining granular design and workflow documentation right alongside your code

I hope you will give it a try, and that together we'll continue to find new best practices to build into our tools and share with each other.

---

# Thank You, <small style="font-size: 0.55em">WordCamp Europe!</small>
<!-- .element: class="align-center" -->

<hr style="margin: 1.5em 0">

Slides: [talks.kadamwhite.com/wceu2018](http://kadamwhite.github.io/talks/2018/wceu)

<!-- .element: class="align-center" -->

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

<!-- .element: class="align-center" -->
<img src="images/hm-logo.png" style="margin-top: 0; height: 3em;" alt="Human Made Logo" />

<!-- .element: class="align-center" -->