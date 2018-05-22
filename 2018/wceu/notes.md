

I'm going to make a statement — possibly controversial — that programming itself is not hard. It's 2018, and we have the best tools we've ever had for writing useful, powerful applications.

What's hard is all the stuff we have to do before and after we write the code -- the documentation, the bug reports, the interpersonal communication.

If this is the hard stuff, we should be talking about it more -- and that's the genesis of this talk. How do we introspect and figure out where all our non-code stuff could be improved? How do we apply the same level of rigor to our bug reports that we do to actually solving those bugs?

If this sounds like project management, and you think, that's not my job, then just remember that project management is a shared responsibility.

---

Reading code is one of the most important skills we learn as programmers, but most of us are faster at digesting words and pictures that describe how something will work, than we are at puzzling it out from code.
Use screenshots and add steps to reproduce to your PRs, even brief, and the pull request becomes a record of the behavior of the application over time.

---

## `.github/PULL_REQUEST_TEMPLATE.md`

```
**Checklist:**

- [ ] The code respects [coding standards](/myorg/myrepo/wiki/Coding-Standards).
- [ ] The code is covered by [unit tests](/myorg/myrepo/wiki/Unit-Testing).
```

---
## Gutenberg's `.github/ISSUE_TEMPLATE.md`
```
## Description
<!-- Please describe what you have changed or added -->

## How has this been tested?
<!-- Please describe in detail how you tested your changes. -->
<!-- Include details of your testing environment, tests ran to see how -->
<!-- your change affects other areas of the code, etc. -->

## Screenshots <!-- if applicable -->

## Types of changes
<!-- What types of changes does your code introduce?  -->
<!-- Bug fix (non-breaking change which fixes an issue) -->
<!-- New feature (non-breaking change which adds functionality) -->
<!-- Breaking change (fix or feature that would cause existing functionality to not work as expected) -->

## Checklist:
- [ ] My code is tested.
- [ ] My code follows the WordPress code style. <!-- Check code: `npm run lint`, Guidelines: https://make.wordpress.org/core/handbook/best-practices/coding-standards/javascript/ -->
- [ ] My code follows the accessibility standards. <!-- Guidelines: https://make.wordpress.org/core/handbook/best-practices/coding-standards/accessibility-coding-standards/ -->
- [ ] My code has proper inline documentation. <!-- Guidelines: https://make.wordpress.org/core/handbook/best-practices/inline-documentation-standards/javascript/ -->
```

## Gutenberg's `.github/PULL_REQUEST_TEMPLATE.md`
```
<!--
BEFORE POSTING YOUR ISSUE:
- These comments won't show up when you submit the issue.
- Try to add as much detail as possible. Be specific!
- Please add the version of Gutenberg you are using in the description.
- If you're requesting a new feature, explain why you'd like it to be added.
- Search this repository for issues and pull requests and whether it has been fixed or reported already.
- Ensure you are using the latest code before logging bugs.
- Disable all plugins to ensure it's not a plugin conflict issue.
- To report a security issue, please visit the WordPress HackerOne program: https://hackerone.com/wordpress.
-->

## Issue Overview
<!-- This is a brief overview of the issue --->

## Steps to Reproduce (for bugs)
<!-- Provide a link to a live example, or an unambiguous set of steps to -->
<!-- reproduce this bug. Include code to reproduce, if relevant -->
1.
2.
3.
4.
<!-- Provide what browser you are using and any other specifics to your setup -->

## Expected Behavior
<!-- If you're describing a bug, tell us what should happen -->
<!-- If you're suggesting a change/improvement, tell us how it should work -->

## Current Behavior
<!-- If describing a bug, tell us what happens instead of the expected behavior -->
<!-- If suggesting a change/improvement, explain the difference from current behavior -->

## Possible Solution
<!-- Not obligatory, but suggest a fix/reason for the bug, -->
<!-- or ideas how to implement the addition or change -->

## Screenshots / Video
<!-- Visual records are oxygen for others to understand what you are sharing -->

## Related Issues and/or PRs
<!-- List related issues or PRs against other branches -->

## Todos
- [ ] Tests
- [ ] Documentation

```

---

T

PHP * Composer * Node * npm
Vagrant * Virtualbox * Docker
macOS * Windows * Linux

What tools do you need on your host computer to run the application? And do they work on all operating systems? If you're hiring contractors or freelancers, or even if you permit OS diversity within your team, somebody's going to end up the odd one out.


You want production data to replicate bugs, so you need an anonymized export


---

---


---

What do we test?

- How the application works
- That a bug has been fixed
- That business goals are met

We don't have tests for, is this easy to work on.

Debugging (murder mystery metaphore): https://twitter.com/fortes/status/399339918213652480?lang=en




"The title of the talk is of course what we forget to test, and you may have noticed that I didn't technically share any tests.



---

## We test our code...
### How do we evaluate the rest?

???

These are the hard parts. It's harder to hold interpersonal processes to the same standard we use for our code; we don't have linters for documentation quality or pull request descriptions.

It's easier to improve a technical process with tools than 
It's easy to build tools to improve our code, but But all our tools are oriented towards code. I think it's a problem that we focus on that to the exclusion of these other parts of our day-to-day jobs.

I want to share some best practices we can use to evaluate and improve our processes; think of it as a style guide for everything that isn't code.

I don't have all the answers, and different teams require different processes. but we'll focus today on two important, complementary things: how we ramp up on a project, whether we're onboarding ourselves or helping our colleagues join the team; and how we improve communication within our teams to facilitate code review, task switching and handoff.
