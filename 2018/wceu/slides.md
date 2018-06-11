# <small>What We</small> Forget To Test
<!-- .element: class="align-center" -->

<hr style="margin: 1.5em 0">

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

<!-- .element: class="align-center" -->

<img src="images/hm-logo.png" style="margin-top: 0; height: 3em;" alt="Human Made Logo" />

<!-- .element: class="align-center" -->

???

Thank you!

What the title of this talk means is that I don't think programming is the hard part of what we do.

---

### Team Communication
### Context Switching
### Project Handoff
### Documentation
### Code Review
### Bug Reports
### Onboarding

???

The hard part's everything we do _in between_ the small periods when we're writing code. These other challenges we face on every project.

We don't have unit tests or linting for any of this.

---

# Markdown Documentation

???

What we do have is our documentation. And I think the humble markdown files in our repositories are under-appreciated.

I was talking to another developer recently and I happened to what they did for documentation at their company. "just README files," they replied, sounding embarrassed.

You should _never_ be embarrassed of your documentation! The hardest part is writing it. And if we take even a tiny bit of time to write our processes down, these simple files can have a major impact on project success.

---
<!-- .slide: data-background="images/example-bad-pr.png" data-background-position="center top" -->

???

We write documentation for interfaces or APIs, but we can also document process. By doing so, we can see where our process is failing.

As an example, take a pull request like this one. There's no description explaining what's being changed, or how I should test it.

If I'm asked to review this code, the best I can do is skim it for obvious logical errors; I can't say whether I think it's a good solution to a problem, because I don't know the problem it solves.

---

### <small>What Makes A</small> Good PR?

- Summarize the issue being addressed
- Link to the acceptance criteria or requirements
- Contain screenshots of before/after changes, or gifs showing interaction
- Explain any unusual design decisions
- List specific testing instructions as needed

???

A thorough written explanation, with screenshots or gifs of screen recordings where appropriate, would have given me the context I need to do a thorough review.

To review code is to step into somebody else's thought process. It's a context switch.

---

## Context Switching <small>Humans Are Not Good At It</small>

_Leave instructions to help your team pick up where you left off!_

???

Context switching and multitasking are things we as humans are _not good at_.

When we take an extra five minutes while opening a PR to give our teammates some background, they can dig in to that code faster and deeper.

Leaving these things out, on the other hand, introduces back and forth, which can take days in a team distributed across time zones. Better team communication saves everybody time.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-pr-template-detail.png" -->

???

How do we ensure we actually do this? Documentation.

GitHub supports creating markdown file templates that control what we see when we open pull requests or issues.

These template files can include HTML comments that are hidden in the final output, but that convey instructions to help ensure the ticket or PR description is thorough.

---

## Don't Make Your Colleagues Guess

_(It will help you, too)_

???

Without templates we often get vague issues, because even with best of intentions we're usually in a hurry and don't want to take the time to go into detail.

_Especially_ with open source projects, more detail is better! Your potential collaborators won't know how best to help you unless you tell them what you need to know.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-issue-template.png" -->

???

Gutenberg's issue template, for example, reminds bug reporters to include

- what they expected to happen,
- specifics about what went wrong, and
- steps to reproduce a bug.

I try to put as much detail and supporting information into my tickets as possible.

Even if I'm writing an issue I'll be working on myself, writing down what I know _now_ creates an on-ramp I can use to get back up to speed when I return to the bug.

---

### Write Your Process Down

_Documented process makes a healthy team_

???

So, write your process down, and update it as needed. Not every template section will be relevant for every ticket, and that's OK!

Our goal is to reduce ambiguity, not to force extra work.

A good issue template defines the standard of communication we want for our team. It reminds us to respect our colleagues' time as we would our own, by being specific and direct.


---

## Colocated Documentation

_Keep documentation close to the task or code it documents_

???

A template can do this because it's _right there_ when we go to open a PR. They have a visible impact on team behavior because they're unavoidable.

In our code, we like type annotations because they're documentation we cannot escape. Prose documentation works the same way: the proximity of the _documentation_ to the _task_ being documented is key.

You may know the saying, "out of sight, out of mind" -- if it takes too long to look up how to do something, that documentation is worthless!

This is why I'm such a fan of markdown files, because they fit right alongside our code in our existing projects.

---

# README.md

- What Is This For?
- How Do You Use It?
- How Can I Run It Locally?
- Where Are The Docs?

???

The humble README is a great example. This is an incredibly important document within your repository -- It's the first thing potential users, contributors, or new teammates see.

A README is your project's landing page and cover letter, and it has to clearly explain what the project is for, how it works, and how to participate in it.

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme.png" -->

### What Is This For?
<!-- .element: class="align-right blackoutline" -->

???

We're probably most aware of the READMEs for open-source libraries we use, because they're what we see first on GitHub or NPM.

I like README's like Redux's, which contain almost excessive detail: not just a brief blurb on what Redux is and why you should use it,

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

_The READMEs for an NPM module, a theme or plugin,  
and a client project have different responsibilities_

???

This type of README is appropriate to a project like Redux that defines an architectural pattern you'd be using throughout your codebase.

However, different types of projects raise different questions, and what is required of the README file depends on that context.

---
<!-- .slide: data-background-position="center top" data-background="images/hm-website-setup.png" -->

???

The READMEs for our client work at Human Made therefore focus on defining team roles & responsibilities and explaining the on-boarding process. These are the key questions we have to answer if we need to hand the project off within our company, or onboard a new contributor from a client's team.

We've gone so far as to build a README generator, to ensure each new project kicks off with all the right baseline documentation in place.

---
<!-- .slide: data-background-video="images/gutenberg-readme-overview.webm" -->

???

Gutenberg's readme, by contrast, emphasizes the project's goals, philosophy and roadmap. For a project like Gutenberg the "why" and "what" are the most important questions, so it makes sense to emphasize these points.

The README doesn't have to do everything: to keep the focus on what matters, Gutenberg's setup and development workflow steps are shifted into other files.

---

## CONTRIBUTING.md: <small>What Do I Need To Know?</small>

- Code of Conduct
- Community & Behavioural Expectactions
- Development Dependencies
- Workflows & Guidelines
- Chain of Command
- Release Process

???

One of these files is CONTRIBUTING.md, a semi-standard filename where you can put everything a developer will need in order to dive into the project.

This includes technical information like local development environment setup instructions, but also information about project management, team roles, workflows, and behavioral expectations.

---
<!-- .slide: data-background-position="right center" data-background="images/gutenberg-contributing-callout.png" -->

???

I love what GitHub does with these files, because if a CONTRIBUTING.md or CODE_OF_CONDUCT.md is present in your repository then they will be highlighted whenever a new contributor goes to open an issue or PR.

Just like with issue templates, this puts a link to the documentation right where it will be of most use to the person who needs it -- by documenting the process alongside our code, our tools can ensure it gets seen when it needs to be.

--

### Encourage Contributions!
<!-- .element: class="align-center" -->

> <small>Thank you for thinking about contributing to WordPress' Gutenberg project! If you're unsure of anything, know that you're <strong>100%</strong> welcome to submit an issue or pull request on any topic. The worst that can happen is that you'll be politely directed to the best location to ask your question, or to change something in your pull request. We appreciate any sort of contribution, and don't want a wall of rules to get in the way of that.</small>

???

I think one nice thing the Gutenberg team does here is that they open their CONTRIBUTING file with a welcoming message that encourages participation. It's important to remember that contributing to open source can feel really hard or intimidating, so do what you can to make people feel comfortable asking questions.

And please, please be nice when you close off-topic issues!

---

### `README.md`
### `CONTRIBUTING.md`
### `CODE_OF_CONDUCT.md`
### `docs/**/*.md`
## _`**/*/README.md`_

???

Projects like the WordPress REST API, Gutenberg, and Redux provide their website or handbook content as a folder of markdown files, but we can go further and sprinkle documentation throughout our project, wherever we need it.

We break our projects up into themes, plugins, modules, and components, so why not give each module its own README?

---
<!-- .slide: data-background-position="left top" data-background="images/readme-files-in-gberg.png" -->

???

This is something else that the Gutenberg project does to good effect. If you search the repository for .md you'll find README files throughout, each one explaining what's going on in a specific folder.

Inline code documentation explains _what_ your code does — these files complement those inline docs by explaining _why_ and _when_ you'd want to use that component.

These README files get displayed as we browse our project code, and they can also be picked up by component development tools like React Styleguidist and Storybook.

---

## Documentation-Driven Development
<!-- .element: style="font-size:2.8em" class="align-center" -->

???

If your docs are kept next to your code in the same repository, it's easy to remember to update the docs when you update the code — or you can go even further, and write the docs _first_.

Imagine you need a new feature. Instead of starting with code, create a markdown file in an empty directory.

Fill out that file with architectural notes on the challenges you face, how your team expects to approach them. Explain the API you intend to build as you would to a user, and you'll spot issues before you even begin to code!

You're giving yourself a chance to think through the project without the overhead of constantly changing code every time you change your mind about something.

This file will live on as part of the project when you do begin writing your unit tests and implementing the feature, and in the end, that markdown file becomes the readme for the new functionality.

---

### README.md <small>is your most important file</small>
<!-- .element: class="align-center" -->

> READMEs are often the single source of documentation that users will come across
> 
> <small><em>~ Gabrielle von Koss, JSConf EU 2018</em></small>

???

So at the very least, even if you do not write dozens of nested READMEs, CONTRIBUTING.md files, issue and pull request templates,

do not underestimate the README.

Every project should have a README, and it should be considered in as much depth as the code it documents.

Documentation does not _have_ to come first, but it is not acceptable for documentation to be an afterthought.

---

## <small>You Don't Need To Use</small> Markdown Files
<!-- .element: class="align-center" -->

<br>

## <small>This isn't only relevant</small> on GitHub
<!-- .element: class="align-center" -->

???

Nothing we've discussed today is GitHub specific or Markdown specific. The message is simply to write things down _somewhere_.

If you want to encourage contribution from team members without write access or if you need to coordinate one set of docs across multiple repositories, consider putting your docs into a wiki.

Or you can write your docs in a CMS, like we do with the WP handbooks — although this introduces permissions issues that make it harder to accept contributions.

---

## Take The Time <small style="font-style: italic;">to write things down</small>
<!-- .element: class="align-center" -->

<br>

## Take The Time <small style="font-style: italic;">to keep docs updated</small>
<!-- .element: class="align-center" -->

???

Documentation doesn't happen unless you make time for it. What we've discussed today is the tip of the iceberg of the benefits of writing and maintaining granular design and workflow documentation right alongside your code.

---

### WriteTheDocs.org
<!-- .element: class="align-center" -->

> From the perspective of a user,  
> if a feature is not documented, it does not exist.   
> If a feature is documented incorrectly, then it is broken.

&ldquo;Documentation changes are cheap,  
code changes are expensive.&rdquo;
<!-- .element: class="align-center" -->

???

I'd encourage you all to check out a website and community called WriteTheDocs; they produce a ton of really valuable information about documentation best-practices that I've come to really value.

---

### This Has All Been Said Before

- ["Documentation-Driven Development"](https://medium.com/blacklane-engineering/documentation-driven-development-8b2ff119104f), Blacklane Engineering, 2017
- ["Documentation-Driven Development"](https://niccokunzmann.github.io/blog/2016-06-10/Documentation-Driven-Development), Nicco Kunzmann, 2016
- ["Readme Driven Development"](https://ponyfoo.com/articles/readme-driven-development), Nicolás Bevacqua, 2015
- ["About API Documentation"](http://www.writethedocs.org/guide/api/about-api-documentation/#id1), WriteTheDocs
- Your own blog post, next month? :)

???

The idea that writing documentation makes you a better programmer is not new, but we keep having to re-learn it.

I hope you'll take the time to give your documentation the attention it deserves, and that you'll share your successes so that others will do the same.

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