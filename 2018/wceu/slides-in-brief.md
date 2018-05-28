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

We could have put these guidelines in a wiki, but nobody would read it! the further we have to go to figure out what we're supposed to do next, the easier it is to get distracted!

The markdown files in our repositories give us so much power to put documentation right where it's needed -- right next to the code.

At Human Made we work on an async team. We can't rely on slack or video chat much of the time. To quote my colleague Joe McGill, if you need to let people know what they need to know, write it down -- and if you need to make sure they see it, write it down as close to the thing they're going to interact with as possible.

We like inline documentation within our code. Learn to love these markdown files in your repo too.

PR's just the tip of the iceberg. You can make issue templates, as well -- these exist for other issue tracker systems too, but GitHub's are again local markdown files.

All too often I see an issue template more or less ignored; they'll say, just, "refactor that thing." What thing? How?

We do this because we're in a hurry. we're opening the issue when it occurs to us; but we're in the middle of something else, and we don't want to break our concentration.

But I'm a firm believer in putting as much detail and supporting material into a ticket as possible. This is frequently the point where we know the most about a bug or a new feature; fill things out, so that when you return to it you won't have to repeat any investigation!

Especially with open source projects, you're not going to be in the same mindspace when you come back to an issue. If you're leaving descriptions for future enhancements, go all-out.

Even if you're just trying to document a minor refactor in a client project, it's worth being thorough; one stressful meeting can knock all of your accumulated ideas out of your head and make you start over!

And starting over's hard. Joining a brand new project is the worst; even if you use a consistent toolset like "react and redux on top of WP", we can't be effective until we've got an environment up and running and know what we're building.

When we come to a new project, the first thing we see is the README, yet another markdown file. This one's the best of all: README's are incredibly important. They serve as your code's landing page and cover letter.



