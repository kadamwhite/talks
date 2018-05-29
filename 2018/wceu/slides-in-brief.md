What we forget to test.

What does that mean?

This talk has evolved somewhat since I proposed it, and I've gone through a lot of titles that would have been better than what's in the program. But in short, I'm here to argue that we spend too much time talking about code. Code's fun, but I don't think it's the hard part of what we do as software developers.

The part part's everything we do _between_ the small periods when we're writing code.

We've got good tools for evaluating our code, but there's no unit tests for team communication; no linting for pull request discussions or onboarding instructions.

Fortunately we CAN evaluate the documentation we leave ourselves to help with these processes. And that's what I'm going to talk about today.

This talk occurred to me when I saw a bad PR.

What's wrong with this? Well, what's written here is good -- it's useful to have PR templates to list things that you want all PR's to have.

But, I could tell that this passed lint and had tests by checking the CI results and 

Doesn't tell me what's being addressed

Doesn't tell me what or how to test (even if you don't consider that part of your code review process)

What makes for a good PR?

- What issue is being addressed?
- Where can I go to find AC or requirements?
- Screenshots of before/after, or gifs showing interaction
- Explanation for any unusual design decisions
- Any specific testing instructions, such as whether we need to set up sample data in a specific way or install newly-added dependencies.

Fleshing out PR's may feel like it's a waste of your time, but you're asking your colleagues to do the harder part: to stop what they are doing, and try to understand your code.

We can suss much of this out from the code, but we're all faster at reading prose. Leaving them information is not just kind, it's critical to good team communication. Leaving things out just introduces back and forth, which can take days across time zones.

If you're doing code review, you're stepping into somebody else's thought process. It's a context switch.

Context switching and multitasking are things we as humans are not good at.

Take an extra five minutes when you're opening a PR to give your teammates as much help as possible.

How do we ensure we actually do this? We leave ourselves instructions, right in the PR description window.

We use GitHub's PR templates to document our process and remind us of the communication quality standards that we have for ourselves and our teammates.

The markdown files in our repositories let us put process documentation right where it's needed -- right next to the code!

We can do this for issues, too. we want to avoid issues that just say, "refactor this," or "that thing is broken." What thing? How? Issue templates help remind people to include what they expected to happen, specifics about what went wrong, and steps to reproduce a bug.

Without templates we get vague issues because we often open them quickly while they occur to us, when we're in the middle of something else. What I had to do seemed clear at the time, and I was busy, so I didn't go into detail.

But now if I had to come back to this three sprints later, I'm toast. Where do I start? I have to reassemble everything I knew about the relevant part of the codebase before I can get back to where I as before. It takes a lot longer than it would have to just write it down in the first place.

I'm a firm believer in putting as much detail and supporting material into tickets as possible. Putting in the time to write a good issue leaves me an on-ramp I can use to get back up to speed.

Especially with open source projects, you're not going to be in the same mindspace when you come back to an issue. If you're leaving descriptions for future enhancements, go all-out!

Even if you're going to tackle the issue soon, it's worth being thorough; one distraction or a long meeting like a sprint retro can knock all of your accumulated ideas out of your head and make you start over.

Issue and PR templates let us hold our team process to a common standard. They save time and they improve communication.

The further we have to go to figure out what we're supposed to do next, the easier it is to get distracted. We could have put these guidelines in a wiki, but nobody would read it! By putting the steps right there in the PR description text area, GitHub ensures we can't miss it. It's our loss if we don't use the feature well. Two markdown files can do a lot of good.

I'm not against wikis, but in the remaining time I'd like to talk about an even better markdown file -- the humble and under-appreciated README.md.

READMEs are your code's landing page and cover letter.

In my opinion a good readme has the responsibility to

- Tell you what a project is and is for, concisely and clearly;
- Tell you in brief how use the project;
- Provide or link to directions for running the project locally; and
- Provide or link to more comprehensive documentation.

I like README's like Redux's, which contain everything but the kitchen sink: not just a brief blurb on what Redux is and why you should use it, but also a philosophy statement, a "the gist" quick-start guide, links to comprehensive documentation, a copious set of examples and tutorials including a video guide, and best of all, a section about when Redux might NOT be the best choice for your project!

But even if you don't do all this, 

GitHub has also introduced CONTRIBUTING.md to share some of these responsibilities.




You're not limited to one README. We encourage code modularization, and each module has its own design constraints, quirks, usage instructions and background. Document that in a README, too!

One of my colleagues at Human Made and a fellow core contributor, Joe McGill described to me recently how he has sometimes seen features begin as a text file in an empty directory. That file contains architectural notes on the challenges and how the team expects to approach them, and it lives as part of the project while they write the code around it. In the end that markdown file becomes the readme for the new functionality.

Documentation-driven development, I guess you could call it!

When nested within individual module folders in your codebase not only will the README text be picked up when you browse to that folder in Github, but it can also be integrated in tools like React Styleguidist and Storybook.

This is not something we do often in core, but it's actually what the Gutenberg




Why _wouldn't_ you want to embed your docs locally in your repo?

The benefits of a wiki include that you don't have to have write access or be able to PR to update docs. But if there's any sort of log-in step required, such as with the WordPress handbooks, a public repo offers better collaboration IMO






Documentation doesn't happen unless you make time for it. What we've discussed today is the tip of the iceberg of the benefits of writing and maintaining granular design and workflow documentation right alongside your code; I hope you will give it a try, and that together we'll continue to find new best practices to build into our tools and share with each other.

Thank you!