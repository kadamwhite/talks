- rest
- history
- origin of the project (rmmcue)
- merge
- successes 
  - gberg
- drawbacks
  - focus miscommunication
- Recent wins
  - meta
  - perf
  - fields
- big gaps
  - batch actions
  - perf
  - more resources / full-site editing
  - persistent misunderstanding
  - context clarification

tbj: 

- look at woo, folks who shipped their own rest api before core, and have adapted to use core infra; may be other projects that are like that. "this is how it's made dev easier/more standard"
- biggest thing, we still don't have component maintainers maintaining their own routes. comments is an example, but terms/taxo's is better example
  - but that would require a lot more standardization / established patterns to be known across groups. g'berg team deviated from this when they do their own endpoints, they persistently do things differently (block renderer has some issues, wp_blocks, etc)
- As component maintainers we haven't established enough of a formal pattern to make it easy for component maintainers to begin _doing_ that
  - blocks directory v1 was written by somebody new to both WP and g'berg, but even after dion re-wrote it the endpoints don't really look like other REST endpoints (not really REST-structured, very specific to gutenberg: it's a plugin-specific instance)
  - The danger of not having this documentation is that the REST API was meant to be a standard, consistent language; without the docs we're already reintroducing these quirks
  - With the editor, a lot of their solutions are VERY tightly scoped to the editor.
  - This is the biggest danger in the future of the REST API; we don't have bandwidth to develop endpoints, and ALSO don't have documented formal patterns / oversight on this development
  - lots of assumptions that the REST API team is hostile towards new endpoints ("highly unlikely" comment from gh)
  - What we want is, if we have to introduce plugin endpoint, do it "properly"
- block renderer is one of the best examples of how things have gotten out of hand. 
  - **THING TO LOOK AT**: (two options: oneOf, and remove schema entirely): tbj gave a talk called schema-driven interfaces (slides on site), he likes experiences like Vienna, driving as much of a client interface as possible from a PHP schema.
  - Pattern of what fields are governed by auth, and that mechanism, is very powerful
  - This will be relevant for a block controller. Issue of supporting 3rd-party blocks in a non-WP environment is hard. Don't want to load untrusted JS into calypso, etc. If you have the schema you can auto-gen an experience that is not as powerful, but functional
- If you have ever run woo, it registers 60 routes; if you just ask wp-json you get them all. more concerned with matching performance than having a lot of routes. (**look up that ticket again**)
- (unrelated? https://github.com/WordPress/gutenberg/pull/18760#issuecomment-561794420)
- As much as we as the REST API team say we want to be RESTful, we don't do it ourselves; we follow PUT semantics, not PATCH
  - TBJ wants to follow standard but is in disagreement here: after the back and forth, "when he found out what he meant", https://github.com/WordPress/gutenberg/issues/17864#issuecomment-559331681
  - Previously for meta, they would only push new values. In 5.3 g'berg puts the existing object back. race condition issues, etc. (prob unreported so far because it only effects enterprise). Their implementation is to change the REST API. Timothy's is to change the client.
  - **TODO: Weigh in**
- TBJ more conservative about what constitutes breakage than some. This is not a bad thing. This is an advantage of having REST separate from G'berg, for perspective, but there's also two pages of g'berg REST issues

Biggest gaps? Biggest issues?

- Batch editing
  - Woo (GET, Post, Put, all) & WP.com (multi-resource get only) have a batch endpoint
  - Timothy's implementation for licenses does a patch request to collection endpoint. Would love to see JSON PATCH support (json patch RFC); we advertise post/put/patch for all editable requests already.
  - (would backbone use a JSON patch? or a put with an incomplete object?)
- Proper JSON patch, related to the above
- Being able to DELETE to a collection (like a list table action: apply this change to a set of include IDs, a specific status)
- Authentication on the client; I can restrict update request based on a parameter and g'berg doesn't know about it. Like restricting to a particular author. gutenberg checks assigned author, rather than looking in the schema for the perms checks associated with the relevant properties.
- T's general sense is, how much can we express in the schema? let's express as much as possible. Structured data seems the only way to do all the perms things we have without a weird meta-endpoint to handle capabilities
- Error handling in general is broken. If you edit a post with one bad metadata value, you get a generic error, but a partial update has been applied and you don't know what it is. If you have multiple meta fields that get updated, you need to send the update, get a response, try again, get an error on the other property, keep iterating, to figure out what's wrong. Need a way to reflect a partial success.
  - REALLY broken for create. The only safe way to create in the REST API is to create a draft post that's empty and get an ID, and then send more data once you have that ID so you can retry
  - **TBJ has a ticket for this**
- Gary's ticket for the settings controller, was to introduce a v2.1 controller. Reading phil sturgeon's screed about API versions, 2.1 is the worst way. "In all honestly the biggest thing we need to figure out is if we can version at all. The only time I think we can do it would be content type negotiation. Stripe has a talk about how they handle versioning, internally at least. They apply a series of transforms for a request, it'll come in to a certain version and it'll get transformed into the next version until you get to stable code. content type negotiation could help; solving wp_error might look like implementing what RYan proposed ages ago, having the error extend from or implement http response.
- Biggest question we have is, we can implement anything; but how long will it be good for? how durable is it?
- Authentication would be awesome for TBJ and anybody else working on plugins

Wins?

- schema usage, patch, etc is easy to implement because infra is so flexible. So it can be addressed within an endpoint.
  - But, the downside is that you get different implementations, so you lose some of the benefits of a rigorous system that all works the same way. Not everything in wp-json/ will or can be consistent.

What does TBJ think I should really hit upon?

- First thing we talked about, responsibility as a team to generate guides for core to make use of. Our biggest blocker is that we have very little resources, we've tried hard but we don't have many contributors. WP in general is sort of "Sergei, then no one, then everybody else"; some VERY active contributors to Gutenberg, etc, and everybody else's contribution is very light. We have no technical project leadership. New contributors are great but it takes a lot of effort from maintainers to give them a good experience too and then only a small % of them recur.
- Data security FUD
- TBJ not bold enough to look at new contributor stats _vs_ a8c employment.
- It would be good to have not just using the api, extending the api, as their own bit of the dev reference; we need "contributing to the REST API" as a section. no real precedent for this in core.
- It takes about five years for TBJ to know the core patterns and be able to apply them. That's true of most of WP, but it does encourage a brain trust. How do we outsource?
- **TODO:** Look at dan abramov's tweet or blog post recently about project philosophies. Right before a discussion of let and const.

Folks to talk to

- Ryan
- Helen
- Somebody at Woo? (Kelly?)