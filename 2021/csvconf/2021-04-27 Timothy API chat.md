**What's new?**

- Did a lot last year
- Biggest thing is auth; added another few endpoints in 5.7.2, introspection endpoint, "give me info about the mechanism by which I am authenticated" and also delete that password
  - Hope had been for 5.8, to take first steps on Scoping: right now you inherit all permissions the user has, which aren't always desired. 
  - In 5.6, worried that user would give an attacker access to their site. Scoping would introduce a base set of permissions, and can be really noisy when requesting advanced caps
- Biggest area they need help is documentation side. "Best we have for auth is george's integration guide that got posted on make.core in Decemeber, when it launched. We don't have the plethora of example code integrations, which would be a great place for a non-technical contributor to jump in."
- Did some good bugfixing in 5.6, 5.7 was lite, 5.8 will be "huge" with the full set of menus and widgets endpoints, some endpoints specific for FSE, and some general block editor endpoints
- Gutenberg people have been getting better at handling REST API stuff, "we're not at the point yet where the REST API team can be the team that tries to coordinate or do final approval on [G work]," but G devs more confident writing REST Code.
  - Are these G specific?
    - 2 main cases: widgets endpoint, and block editor settings endpoint. Editor Settings is very Gutenberg-specific. Widgets endpoint, noisysocks has been doing refactoring, has been aware it shouldn't be hyper-specific to Gutenberg. "Getting better in that regard."
    - G is the main driver for widgets, but "structure of that endpoint" could be used in other applications.
    - Menus for 5.8, editing interface won't land in 5.8; but full side editing has a menus block, that block doesn't talk to REST API, it's block based. But it uses REST API for importing "legacy" menus.
  - Edit context forced on anything in core/data, was an issue with some third-party endpoints. core/data is moving towards default list of query params to be appleid to certain API resources; also helps make endpoints less specific to editor code

**Any other significant contributors?**

- Team is "really skinny". "that continues to be the biggest issue."
- "When we did the [auth] merge, George got brought up into a bunch of other stuff. Most of the app passwords merge stuff fell to [timothy], George is getting a little time back for authentication stuff, but pretty limited"
- Have had a couple new contributors showing promise, "there was a weird thing with Jonny, who was working with someone at XWP and getting him involved -- Lucas P??, who did some good work. The weird thing was related to a couple of endpoint stuff, and general upset-ness that menus aren't in core. There was a weird trac ticket where lucas was working on a patch, and then Timothy gave feedback, and then Jonny re-wrote or re-submitted a new thing on its own even though he was the one asking Lucas to get involved. Yeah."
- There's really been a good contributor, Sergei Jakumun (sp?) who's done great work on JSON schema stuff, our JSON schema support is much more broad, better, more accurate. He's been doing a lot of the hard work on that front.
- DHH has been doing good work on specific spots

**How're you doing on burnout / enthusiasm?**

- Enthusiasm is the same as normal, 'Well, this is the state of WP, isn't it great?' irony
- We'll see what happens with 5.8, there's a lot of endpoint stuff that has to merge. Usually isn't a problem because the API is more or less stable
  - Hopeful that with Robert and widgets endpoint, Timothy's been able to point out things, have him take care of them, and then approve or not approve. Less of a, "well if this has to happen, like, my example is the 5.3 media stuff, where he's just 'we're shipping this feature' and then realizes before beta 1 that this needs REST integration to work in the editor." "I'm hoping that's not going to be a problem in 5.8"
- It would be a benefit to have more active component maintainers, or committer. Some people are poking around sometimes, SergeyB / Jonathan review some API stuff, but nobody else focused on it. "Jonny got proposed for commit but that stalled out, I'm optimistically hopeful that if that would go through it would be a net benefit."
- "for 5.8, this specific moment in time we're treading water. Part of that is that FSE will bring in so many endpoints but it's not time for that yet." Have 'paused' on REST work for 5.8

**Biggest current gap?**

- Auth docs. Also don't have WordCamps to help evangelize / publicize how to use it. Need sample app examples in a variety of frameworks.

**Biggest shortcoming of originally-merged code?**

- "We probably did need more use-cases in core in 4.7, it's a problem of -- from my perspective, the amount I was involved, we've hit the milestone and got this in core. There was enthusiasm in 4.8, 4.9, then that fizzled out really quickly. That fizzled out before Gutenberg really kicked off [or 'got going'], everybody had put in this energy but was just exhausted.
- "I'm trying to remember... my perspective, we weren't missing much. We were missing things specific to an editor replacement, like revisions. But the fundamentals of the API endpoints themselves.
- "We added Search... most of this isn't things from my perspective that were glaring missing issues. I don't think the lack of... we've talked about this before, it's [biased by] the parts of the REST API i use, I mostly use the backbone, custom controllers. I don't do a lot of work with built-in endpoints. There are things we improved, meta support improvements to make it easier to do custom things [with core endpoints,] but I don't think there were really any.... the way to phrase this, there's nothing where I'd say we should have held up release until the API supported this specific feature. We might have discovered _some_ things [if we'd used it more places right on merge]," but most issues didn't surface until Gutenberg, and that would have been waiting far too long
  - +1 to that, getting it out the door first was essential.
- "The biggest glaring issue" for people was the save hook order Peter implemented in 5.?, and we wouldn't have caught that earlier unless we'd waited to ship the API until 5.0.
- (I might say, filtering, search, meta handling)

**What do you think about the way they've implemented capability checks in the editor?**

- "My pitch has always been for a function that works with the schema, and to be able to do that in a programmatic fashion. I want to edit the Author field in this resource, how can I do that without checking for a link that is "action assign author." Links are attached with a schema, so if you wanted to do that you _could_; could check this property against this validation schema, no, they don't have permission, yes, they do.
- "That's the way I think the functionality should work. We only have half of that, checking for specific actions where we know a field may be locked down, rather than being generic. Does what it does for stock WordPress core stuff, but you can't extend it.
- "Biggest detriment is the refusal to embrace schema documenting. I don't *think* Gutenberg really ever queries the schema, whereas from my perspective they should be embracing the schema because these things are documented in a programmatic fashion. It's very specific to what [Gutenberg devs] are interested in at the time.

**What do you think are the most significant changes to the API since merge outside of auth?**

- "In terms of features, have the dev.wp.org changelog, but none of those features are blockers for users of the API -- consumers of the content. They're just things necessary for people looking to build editor experiences.
- "From my persepctive the biggest feature outside of auth is the plugins endpoint, can now do activation, installation, deletion of plugins from the .org repository. In combination with Auth, that is powerful for SASS experiences. But single-endpoint wise, that was an important feature to add.
- "Aside from that, autosave, better revision support... DUX stuff, better JSON schema support, pulling out reusable functions, stuff like that

**Is Auth in use?**

- I don't think Auth is being used in mobile app _yet_, ping George, he's been involved in getting people over to it.
- Or who knows, maybe we'll end up reverting API authentication. *[Sounds like he's salty]* Mobile team still wants username / password authentication, they don't like the flow. [what we have is still better]
- "We need evangelism from companies that have paid products; Ulysses launched with a WP integration for their editor, but it uses XML-RPC. I don't know what happened there. I don't know anybody there to reach out and say, "hey," and I also don't know whether I can email Ulysses and say, hi, I'm a core member of the WP project team, I work on the REST API, can we talk about [why you did things the way you did]
- "Zapier has WP integration, Zapier has a plugin that just ads an auth mechanism with username/password and then uses core REST API endpoints. A conversation should be happening with them, what would it look like to move this to use app passwords
- "ManageWP uses to have a totally custom auth strategy, now uses app passwords and uses it to install iThemes Sync plugin
- "Talking to Yoast is probably, a thing to check in there, he talked a lot about how powerful an auth mechanism would be, so I assume he'd have something planned

**Biggest remaining gap? Future plans?**

- "I talked with Peter about custom post statuses, which I think is one of the biggest missing parts of the WP puzzle. I don't know how much I'm betraying the complexity of scoping, but I think those are the two things that aren't very dreamy, I guess, but in terms of impact could be really powerful. Having proper authentication scoping, which I think would be very powerful, and custom post status support. Essentially anything that touches the editor _has_ to launch with the REST API, so we [could not launch custom statuses without thinking of the REST API], but a lot of the work there is deep internals where Peter's been working to untangle post status issues.
- "Theres not much missing" in API in terms of core WP constructs, themes, multisite. "[Multisite is] never gonna happen. Multisite is apparently dead. That seems to be Matt's thoughts in the matter, multisite isn't going anywhere for any reasonable amount of time."
  - Three levels of hearsay, Jonny wrote up a multisite roadmap, got told off by Matt.
- Gutenberg is doing everything block-based, or custom post types.
  - The biggest blocker for block exposure via API—block data isn't exposed, just the blocks—and the blocker for that is attribute parsing. That's too slow to do in PHP.
  - "Each block being represented in the database" isn't going to happen, blocks can be attached to posts, CPTs, menus, widgets have a widget block
  - "Everything revolves around, to what degree do we do that on the server," you're limited when parsing blocks.
- "the other thing is dependencies, WP Scripts and WP Styles. There's a desire to, for the block editor to be able to lazy-load certain dependencies, for this handle print me out all the scripts and localized JS and translations and get that over the REST API. But so far they've been making do without it, and loading 500mb of JS on the page at once in the admin."
- "We're kind of open, soon, because I don't know yet whether I plan to ship all the menus in 5.8 or just the GET endpoints—in some regards that'd be safer, but, hmm—at that point, that's all of our core entities modeled. It leaves WP_Scripts and WP_Styles, but that will be more RPC than REST and can be tailored to G
- "other types of things, looking at JSON Schema things, looking at version 6 and version 7. The main breaks are from v4 to v6, mostly around exclusive minimum and exclusive maximum. That's the major breaks, aside from required fields stuff which we've half-solved, of the v3 vs v4 syntax. I'd like to see that upgraded"
- "John has been working on a lot of, building a schema from scratch to represent WP resources"
- "for that JSON Schema stuff, for dates, the way we represent those in the REST API is a mess—somebody decided in 4.7.x or 4.8 to do the worst half-measure. I've talked with John about whether we could do accept-header changes."
  - Versioning... if we introduced a v3, there's a million things that would break. Filters, classes, nothing is version-specific. We have a constant for version, which is 2. We don't use that constant anywhere. If we wanted to introduce breaking features, everything would break, because they'd either need to have a new filter or the data we passed to it wouldn't work because existing code wouldn't expect it.
  - Which means we have to do something closer to how Stripe handles it, the base response is the "best" version and we mutate back to inferior versions if somebody doesn't request it [with a more recent header?]
- ""[but], we really need to fix timezone handling,
- "and where schemas are just wrong. We've had support in core, for mixed schema types, one of, any of. But, I'm afraid to use them in existing spots, for example the content endpoint should be either a one-of object with those properties, or a type of string. Right now, it's just specified as an object and disable validation and handle it all custom because I don't know what could break in terms of how people are passing invalid data now that isn't causing an issue. We have support for documenting these things the correct way, but when we start doing it the correct way we'd be throwing errors [when people aren't doing things right]
- "That's the best answer of what was missing in 4.7, is a thought-out plan around how versioning would work. We didn't have a plan for major-version changes. And I think the reason is, there's not a lot of benefit to bumping the API, because we have to support v2 ad infinitum. But we lie to ourselves by saying "this is v2."
- Woo has endpoint versions, and v3 extends v2 for adding and changing stuff like that. I don't know to what degree it's successful, and I can't remember whether their filters support versions

**Do you have any thoughts on project leadership,** and what could have been done to better encourage participation in specific core components?

- "I've debated signing up for those listening sessions... I don't think the REST API is unique in that we have a dearth of contributors, and that's a major f**king problem. I don't know what other real conversation I'd have.
- "I don't agree with Morton, there are project leadership issues but I don't agree with a WP governance type of deal.
- "I think Matt is too inaccessible, and I don't know where his headspace is at in terms of certain things. The reason Auth got accepted, I think, is that George can chat with matt whenever he wants. (I mean anyone can, but it depends on whether he sends a reply). 
- "were better off in a benevolent dictator model, than a committe model."
- "It would have been far easier for Automattic to have built G internally and made it work only in WordPress.com -- it would have fragmented the ecosystem, but it would have been more successful to them. [So I] vigorously disagree [with the criticism that G is only .com-focused]"
- "For the most part, I don't care. I've never been told not to work on something in the REST API, it's in core, that battle has been fought. Everything I do is related to Gutenberg and is therefore allowed in this specific release because it makes the API better. I'm going to keep doing what I'm doing until somebody tells me I can't work on something"



T built a desktop app with SwiftUI, wp-mail-debugger, that uses the auth stuff.

















