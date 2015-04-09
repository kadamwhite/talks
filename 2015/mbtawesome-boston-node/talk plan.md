- Intro
    + Bocoup
    + How F'd is the T
    + Green-field project

- Going to review the tech used: none of this will be surprising to most

- Used Node
    + At a Node meetup: not surprising
- Express on the server
    + Easy to build what I wanted;
    + I had some familiarity with it
- Postgres & Bookshelf for the database
    + Institutional familiarity via Tyler, etc
- Nunjucks for templating
    + Been curious, wanted to experiment
    + Based on jinja
    + Flexible and supports filters
    + Native Express support
- Backbone on the client
    + Lightweight
    + Didn't need much routing, or complex interaction
    + Data is hierarchical: lines, stations, trains
- Browserify for builds
    + Frustrated with AMD configuration
    + Comfortable with a build step
    + Easy to set up!

- App Demo

- What worked?
    + Node & Express: If it ain't broke, don't fix it
- What changes would I make?
    + First, add commuter rail!
    + And a green line map.
    + (features over tech, even for a side project!)
    + Backbone
        * Ampersand plays nicer with Browserify, and has some nice sugar
    + Nunjucks
        * Picked it b/c frustrated with handlebars, but the tooling (via Browserify) lagged a little behind the library itself.
        * Had to jump through hoops.
        * Will probably eventually re-write to use Combyne; plug for tim's talk!
    + Postgres
        * YAGNI, turns out!
        * No data, just LRU cache

- Thanks!
