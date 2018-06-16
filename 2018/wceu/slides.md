# <small>What We</small> Forget To Test

<hr style="margin: 1.5em 0">

K. Adam White &bull; [@KAdamWhite](https://twitter.com/kadamwhite)


<img src="images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />


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

The hard part's everything we do in between the small periods when we're writing code.
We face these challenges on every project, and we don't have unit tests, linting or web frameworks to help us for any of this.
But fortunately, one of these can help with the rest. 

---

### <small>This is a talk about</small> Documentation

???

So instead of talking code, let’s talk documentation.
Talking to another engineer recently, I asked how they handled documentation at their company. "just README files," they replied, sounding embarrassed.
You should never be embarrassed of your docs! Even a simple markdown file can have a major impact on project success.

---
<!-- .slide: data-background="images/example-bad-pr.png" data-background-position="center top" -->

???

We document interfaces and APIs, but we can also document process. Doing so makes it easier to see where our process fails. As an example, take a PR like this one. 

(advance) There’s no description explaining what's being changed, or how to test it.
If I'm asked to review this, the best I can do quickly is to skim the code for obvious logical errors; I can't say whether I think it's a good solution to a problem, because I don't know the problem it solves.

---

### <small>What Makes A</small> Good PR?
<!-- .element: class="align-left" -->

- Summarize the issue being addressed
- Link to the acceptance criteria or requirements
- Contain screenshots of before/after changes, or gifs showing interaction
- Explain any unusual design decisions
- List specific testing instructions as needed

???

Think about the name Pull Request: if we’re requesting our code be added to a project, we should be explaining what it does. A thorough written explanation, with screenshots or gifs of screen recordings where appropriate, would have given me the context I need to do a thorough review.

Taking an extra five minutes to give our teammates some background will save them a lot of time and questions. Leaving details out, on the other hand, introduces back and forth, which in a globally distributed team like mine can take days across time zones. Better team communication saves everybody time.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-pr-template-detail.png" -->

???

So, how do we ensure we actually fill the PR description out properly? Documentation.

GitHub supports creating markdown file templates that control what we see when we open pull requests or issues. We can use HTML comments in these template files to provide detailed instructions about what details we want to see in a PR or ticket.

---

## Don't Make Your Colleagues Guess

_More Detail Is Always Better_

???

Without templates we get vague issues, because even with best of intentions we're usually in a hurry and don't want to take the time to go into detail. But more detail is always better, especially with open source projects!
Potential collaborators won't know what information you need from them unless you tell them.

---
<!-- .slide: data-background-position="center top" data-background-image="images/gutenberg-issue-template.png" -->

???

Gutenberg’s issue template reminds bug reporters to include what they expected to happen, specifics about what went wrong, and steps to reproduce a bug.

However small the bug, we know more about it when we open the issue than we will when we return to it later. Writing down what we know now creates an on-ramp we can use to get back up to speed in the future.

---

### Write Your Process Down

_Documented process makes a healthy team_

???

If used in this way, issue templates define the standard of communication we want for our team. They reminds us to respect our colleagues' time as we would our own, by being specific and direct.
That standard should never be ambiguous. So, write your team’s process down, and update it as needed.


---

## Colocate Your Documentation

_with the thing it documents_

???

Templates have a visible impact on team behavior because they’re unavoidable—it’s right there when we go to open a PR.
You may know the saying, "out of sight, out of mind" -- if it takes too long to look up how to do something, that documentation is worthless!

This is why I'm such a fan of markdown files, because they fit right alongside our code within our existing projects.

---

# README.md

- What Is This For?
- How Do You Use It?
- How Can I Run It Locally?
- Where Are The Docs?

???

My favorite markdown file of all is the humble README. This is the first thing potential users, contributors, or new teammates see—it’s your project's landing page and cover letter.

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme.png" -->

### What Is This For?
<!-- .element: class="align-right blackoutline" -->

???

We're usually most aware of the READMEs for open-source libraries we use, where they display on the project’s GitHub repository or NPM listing.

A README like this has to clearly explain what the project is for, how it works, and how to participate in it.

I like README's like Redux's, which contain almost excessive detail: not just a brief blurb on what Redux is and why you should use it,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-philosophy.png" -->

### Project Philosophy
<!-- .element: class="align-right blackoutline" -->

???

but also a philosophy statement, installation instructions,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-the-gist.png" -->

### Usage Overview, <br>Learning Resources & Comprehensive Docs
<!-- .element: class="align-right blackoutline" -->

???

a quick-start guide, links to comprehensive documentation, and a copious set of examples and tutorials, including blog posts, video guides, and sample apps,

---
<!-- .slide: data-background-position="center top" data-background="images/redux-readme-before-proceeding.png" -->

### When Should I <br> _Not_ Use This?
<!-- .element: class="align-right blackoutline" -->

???

There is even a prominent section about when Redux might NOT be the best choice for a project!

This is something we never think to call out, but not every tool is appropriate to every task, and that information belongs in our documentation too.

---

## Tailor To The Task

_The READMEs for an NPM module,  
a theme or plugin, and a client project  
all have different responsibilities_

???

I think Redux has a great README. But the README for an open source library has different responsibilities than the README for a client project, theme or plugin.

What information belongs in the README depends on that context.

---
<!-- .slide: data-background-position="center top" data-background="images/hm-website-setup.png" -->

???

The READMEs for our client work at Human Made therefore focus on defining team roles & responsibilities and explaining the on-boarding process. These are the key questions we have to answer when somebody new joins the project.

We've gone so far as to build a README generator, to ensure each new project kicks off with all the right baseline documentation in place.

---
<!-- .slide: data-background-video="images/gutenberg-readme-overview.webm" -->

???

By contrast, Gutenberg’s README emphasizes the project's goals, philosophy and roadmap. For a project like Gutenberg the "why" and "what" are more important than the technical specifics.

The README doesn't have to do everything: to keep the README focused and concise, the setup and development workflow steps get shifted into another file.

---

## CONTRIBUTING.md: <small>What Do I Need To Know?</small>

- Code of Conduct
- Community & Behavioural Expectactions
- Development Dependencies
- Workflows & Guidelines
- Chain of Command
- Release Process

???

CONTRIBUTING.md is another semi-standard filename where we can put everything a developer needs in order to dive into the project.

This includes technical information like local development environment setup instructions, but also information about project management, team roles, workflows, and behavioral expectations.

---
<!-- .slide: data-background-position="right center" data-background="images/gutenberg-contributing-callout.png" -->

???

I love what GitHub does with these files, because if a CONTRIBUTING.md or CODE_OF_CONDUCT.md is present in your repository (advance) then it gets highlighted when a new contributor goes to open an issue or PR.

Just like with issue templates, this puts the documentation right in front of the person who needs it — by storing this information alongside our code, our tools can ensure it gets seen when and where it needs to be.

---

### Additional READMEs <small><em>may be nested in project subfolders</em></small>

???

But we’re not limited to this handful of specific markdown files. We can write full-on user guides or handbooks as markdown in a docs folder, like Gutenberg or Angular do;
but we can also sprinkle small pieces of documentation throughout our project, wherever we need it.
We break our projects up into modules, and components, so why not give each module its own README?

---
<!-- .slide: data-background-position="left top" data-background="images/readme-files-in-gberg.png" -->

???

Again looking at Gutenberg, if you search the codebase you'll find READMEs throughout the repository, each one explaining what's going on in a specific folder or component.

These README files get displayed as we browse the project, and they can be picked up by development tools like React Styleguidist and Storybook. They complement the inline docs by providing an overview of why and when we’d want to use each module.

---

## Documentation-Driven Development
<!-- .element: style="font-size:2.8em" class="align-center" -->

???

If our docs are colocated with our code in the same repository, it's easier to remember to update them when we update the code — or we can go even further, and write the docs first.

Imagine you need a new feature. Instead of starting with code, create a markdown file in an empty directory. Fill out that file with architectural notes on the challenges you face, and how your team expects to approach them.

---

## Documentation changes are <strong><em>cheap</em></strong>, code changes are <em><strong>expensive</strong></em>

<small>~ WriteTheDocs.org</small>

???

Explain what you intend to build as you would to a user, and you'll spot issues before you even begin to code! You're giving yourself a chance to think through the design without the overhead of constantly changing code every time you change your mind about something.

Once you do finally write the code, this file lives on to become the README for the new functionality.

---

## <small>You Don't Need To Use</small> Markdown Files

## <span class="amp">&amp;</span>

## <small>This isn't only relevant</small> on GitHub

???

I’m not here today to tell you you have to do things this way, or that you have to use Markdown. GitHub may do some nice things with these files, but nothing we've discussed today is specific to GitHub or even to Markdown. The message is simply to write things down, and to do so as close to your code as possible.

---

### README.md <small>is your most important file</small>

> READMEs are often the single source of documentation that users will come across
> 
> <small><em>~ Gabrielle von Koss, JSConf EU 2018</em></small>

???

But I do believe that every project should have a README, and that it should be a good. If you want docs contribution from non-developers, you may put most of your docs in a wiki, or a CMS — but the README should still exist, as a visible single point of entry into your project.

---

## Take The Time <small style="font-style: italic;">to write things down</small>

<br>

## Take The Time <small style="font-style: italic;">to keep docs updated</small>

???

We spend _so much time_ talking about code, but just like accessibility, internationalization, and testing, documentation and team processes keep becoming an afterthought.
Documentation does _not_ have to come first, but it is _not_ acceptable for it to be an afterthought.

---

### This Has All Been Said Before

- ["Documentation-Driven Development"](https://medium.com/blacklane-engineering/documentation-driven-development-8b2ff119104f), Blacklane Engineering, 2017
- ["Documentation-Driven Development"](https://niccokunzmann.github.io/blog/2016-06-10/Documentation-Driven-Development), Nicco Kunzmann, 2016
- ["Readme Driven Development"](https://ponyfoo.com/articles/readme-driven-development), Nicolás Bevacqua, 2015
- ["About API Documentation"](http://www.writethedocs.org/guide/api/about-api-documentation/#id1), WriteTheDocs _&larr; Excellent Resource!_
- Your own blog post, next month? :)

???

The idea that writing docs can make you a better programmer is not new, but we keep having to re-learn it. We keep re-discovering how much more effective our teams are if we write down how we want to work together, and stick to those standards.
I hope you'll take the time to give your documentation the attention it deserves, and that you’ll share your successes with others so that they may do the same.

---

# Thank You, <small style="font-size: 0.55em">WordCamp Europe!</small>

<hr style="margin: 1.5em 0">

Slides: [talks.kadamwhite.com/wceu2018](http://kadamwhite.github.io/talks/2018/wceu)


K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)


<img src="images/hm-logo.png" style="margin-top: 0; height: 3em;" alt="Human Made Logo" />

???

Thank you for having me, WordCamp!
