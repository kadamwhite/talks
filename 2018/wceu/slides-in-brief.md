What we forget to test.

What does that mean?

This talk has evolved somewhat since I proposed it, but in short, it means I think we spend too much time talking about code. Code's fun, but it's not the hard part.

The part part's everything we do _between_ small periods of writing code

We've got good tools for evaluating our code, but there's no CI for our non-code processes; no linting to tell me whether a developer handoff or PR review is going to go well.

One thing we CAN evaluate at is the documentation we leave ourselves _alongside_ the code

Talk occurred to me when I saw a bad PR.

(explain PR templates?)

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

Even if you're just trying to document a minor refactor in a client project, it's worth being thorough; one long meeting like a sprint retro can knock all of your accumulated ideas out of your head and make you start over.



We could have put these guidelines in a wiki, but nobody would read it! the further we have to go to figure out what we're supposed to do next, the easier it is to get distracted!

And starting over's hard. Joining a brand new project is the worst; even if you use a consistent toolset like "react and redux on top of WP", we can't be effective until we've got an environment up and running and know what we're building.

When we come to a new project, the first thing we see is the README, yet another markdown file. This one's the best of all: README's are incredibly important. They serve as your code's landing page and cover letter.



