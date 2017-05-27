<!-- .slide: class="notcenter" -->

# Democratizing Software

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Bocoup](https://bocoup.com)

???

Thank you for having me, it is an honor to have been invited. <3 to Portland.

Intros -- get audience feel

When Gary invited me to speak I knew immediately what I wanted to share with you. This talk is a departure for me; I'm used to talking about code. But for the past year or so, as I worked on the REST API project, I've been thinking a lot about what WordPress is for, and more importantly what WordPress actually does.

---
<!-- .slide: data-background="url('./images/democratizing-publishing-slack.png')" data-state="solid-bg" data-background-position="center" data-background-size="cover" -->

???

WordPress core development is coordinated using Slack, and when you sign in to the WordPress slack channel, you see a series of customized messages from the lead developers. There's a lot of cute messages like "Initializing the loop" or "rounding corners," but this one always catches my eye.

"Democratizing Publishing." This is the stated goal of Automattic, the company behind WordPress.com, and it is the closest thing to a mission statement I know for WordPress as a whole.

---
<!-- .slide: class="notcenter" -->

### Democratize

_verb_ | de·moc·ra·tize | \di-ˈmä-krə-ˌtīz\

> : to make (something) available to all people<br>
> : to make it possible for all people to understand (something)

<small><em>~ [Merriam Webster](https://www.merriam-webster.com/dictionary/democratize)</em></small>

???

And it's a good mission. We give people around a world a voice, a place to be heard, an online home -- ourselves included.

Now, that makes sense for publishing. But, to democratize something, our dictionaries tell us, is to make it not just available but _understandable_ to _all people_.

---
<!-- .slide: class="notcenter" -->

## _All People_

???

And that should make you question my title of "democratizing software". Because software is code.

All people. Looking at this room, not much is true about all of us; the WP community is diverse and multivariate.

But we are all human, so we are all born, we all die, and none of us start out knowing how to code.

---
<!-- .slide: data-background="url('../day-of-rest-boston/images/tank-matrix-many-screens.jpg')" data-state="solid-bg" data-background-position="center" data-background-size="cover" -->

???

The word itself presents a problem. To borrow a idea from Mike Bostock, _code_ "suggests impenetrability." Code is "hardly human-friendly;" code is opaque, abstract.

That is of course why we use the word. Computers work in abstract ways, so we invented symbols and programming languages to make it easier for us to tell them what to do.

But that abstraction means the barrier to entry is high. Learning to code is hard. Even in the Matrix, where _every character is literally a hacker,_ there's only one or two dedicated computer users per ship.

---
<!-- .slide: data-background="url('./images/bloomberg-code-year.png')" data-state="solid-bg" data-background-position="top center" data-background-repeat="no-repeat" -->

???

So to democratize software, you have to teach programming.

About half a decade ago we started to hear calls for everybody to learn to code. I don't know that there's anything that _everybody_ should learn; I'm not sure how applicable JavaScript is to a mayor, for example.

But I do believe that everybody should have the _right_ and _opportunity_ to learn to code, when they want to. And they should know what it's good for. It shouldn't be magic.

Programming is, fundamentally, a thought process; it is structured problem solving. There's a lot that you can do with even the most basic skills.

http://www.bbc.com/news/technology-16440126

---
<!-- .slide: class="notcenter" -->

## _&ldquo;The web was supposed to be a think we make&rdquo;_

<em>~ [Anil Dash](https://medium.com/glitch/the-web-was-supposed-to-be-a-thing-we-make-c023b6e7f56a), CEO of Fog Creek Software</em>

???

This was the initial promise of the web. The internet wasn't just something we'd consume, but it was something we ourselves were intended to help to build. It was easy, or at least easier than other types of code.

With a basic knowledge of HTML and FTP -- "that bizarre, magical way in which things are flung into the internet" -- you could make a space for yourself online.

---
<!-- .slide: data-background="url('./images/xkcd-geocities-tribute.png')" data-state="solid-bg" data-background-position="top center" data-background-repeat="no-repeat" -->

???

Companies like Angelfire and Geocities made this easier, providing free hosting and more intuitive editors. But we still build our internet homes ourselves, assembling websites out of spare parts, borrowed images, and rotating text. Sites like Geocities even made the homesteading metaphor explicit, organizing sites into neighborhoods and addresses.

In the 2000's, things got a little easier. Sites like MySpace or Livejournal provided a more consistent base, but you could still hack or theme it to express yourself. This lowered the barrier to entry at the expense of making your site look a little more like your friends' -- theming only takes you so far.

---
<!-- .slide: data-background="url('./images/facebook-signup-screen.png')" data-state="solid-bg" data-background-position="top center" data-background-repeat="no-repeat" -->

???

Taking templated sites to their extreme, we reach the present day. We've traded expression for ease-of-use. Almost everybody's web presence requires no coding at all but looks exactly the same, and cannot be customized.

And this is where most existing system fail. Because sites that prohibit customization restrict curiosity.

---

<div style="width: 80%;margin:auto;">
![How to draw a Doge, from a Vice article that 404's](../loopconf-wpapi/images/how-to-draw-a-doge.png)
</div>

???

We can still find ourself a web host, roll up our sleeves, bust out an FTP client and build something ourselves; but if you try to ask "how do I make a website" in 2017, it doesn't feel like a straightforward process anymore.

It feels like there is some step in the middle that we're not telling people.

---
<!-- .slide: data-background-video="./images/sue-lockwood-tech-choice.mp4" data-state="solid-bg" data-background-position="center" data-background-repeat="no-repeat" data-background-video-loop="true" data-background-size="contain" -->

<small><em>Illustration by [@deathbearbrown](https://twitter.com/deathbearbrown)</em></small>
<!-- .element: class="whitebg" -->

???

Because when you go looking for guides on building websites, you run into all this.

What programming language should I use? Do I really need to learn Ruby, Python, PHP, JavaScript or any of the million frameworks -- my friends just told me I could learn HTML?!

All these tools are aimed at people who already know how to code. Where are we supposed to start?

---
<!-- .slide: class="notcenter" -->

![WordPress Logo](../../2014/wcsf-node-wp/images/wordpress-logo-simplified-rgb.png)

???

And this is where WordPress comes in.

Because WordPress is useful to programmers, but it is first and foremost for writers. This sets it apart from many other open source communities, where the audience and consumers of the software are also technical.

I believe that WordPress, both the software and this community we have built around it, is unique in the web ecosystem in the way it brings the consumers and developers of the software together in one room like this.

---
<!-- .slide: data-background="url('./images/wpdotcom-theme-gallery.png')" data-state="solid-bg" data-background-position="center" data-background-repeat="no-repeat" -->

???

WordPress doesn't want you to make a site that looks like everybody else's. It is about expression. Our theming community is one of our selling points:  Themes and plugins provide a flexible starting point for building your site.

We've still got a lot of work to do to make it easier to find and configure the theme that you want, but nobody can argue that we don't provide a lot of theme choices!

---
<!-- .slide: class="notcenter" data-background-video="./images/customizer-theme-preview_hd.mp4" data-state="solid-bg" data-background-position="center" data-background-repeat="no-repeat" data-background-video-loop="true" data-background-size="cover" -->

### Encouraging Customization
<!-- .element: class="whitebg" -->

???

The work that's gone into the customizer can help with finding a theme that works for you, and it's the first step in easily personalizing your site.

For the developers in the room, if you saw RC's talk this morning, supporting the customizer is one of the most empowering things we can do for our users.

---
<!-- .slide: data-background-video="./images/using-customizer-css.mp4" data-state="solid-bg" data-background-position="center" data-background-repeat="no-repeat" data-background-video-loop="true" data-background-size="contain" -->

???

And it's in the customizer where a WordPress author can most easily first encounter what we would call code.

Last year the customizer gained the "Additional CSS" tab -- we can change our how site looks without leaving the admin by writing CSS stylesheet rules. No FTP, no files, just you and your site.

And best yet, the changes you make are applied in real-time. User interface designers like Brett Victor would be proud.

---
<!-- .slide: class="notcenter" -->

## Learning to Code
### The WordPress Way

???

This is the start of what I'd describe as the _WordPress Style_ of programming education. It's not the only way people we learn, but it's a way that is uniquely enabled by the way WordPress works. It's practically motivated, and incremental. It can happen almost by accident.

---
<!-- .slide: class="notcenter" -->

## CSS
### &nbsp;

???

It starts here: We have a site, we want it to look different. Because WP is a platform that can be customized, we want to customize it. We want to make this little piece of the internet into our own space.

CSS allows us to make that change. Maybe a friend helps us figure out what to write; maybe we get a book, or find a tutorial online. The important thing is that it's a feedback loop that we can _see_.

It's abstract, but maybe it's a little less magic.

---
<!-- .slide: class="notcenter" -->

## CSS
### _is Code_

???

And now we're coding. Now we're using the tools with which this software is made. That's all it takes.

Some software engineers would say that CSS is not code. That's ridiculous. CSS is a complex and rich language that, in the right hands can work wonders. And yet I still regularly hear friends -- and even colleagues -- put themselves down because they "only know CSS."

We have to fight this attitude, and encourage each other to celebrate how impressive it is to control the way a webpage looks.

---
<!-- .slide: class="notcenter" -->

## HTML

???

CSS can work wonders but it can't change the content on the page. At some point many of us found ourselves wanting to move deeper than presentation, to rearrange or augment the structure of our site.

Our themes are open source, so we can tweak them, changing things to taste. Theme files are mostly HTML, so it's not too intimidating.

---
<!-- .slide: class="notcenter" -->

## PHP

???

And while we're editing our theme templates we might begin to intuit or study what these other pieces of code do inside our themes. We begin to learn and use template tags and the loop.

WordPress is written in the PHP programming language, which at first just looks like fancy HTML. Later on we can learn about functions child themes and code organization, but we have to start somewhere.

---
<!-- .slide: class="notcenter" -->
## JavaScript

???

Or maybe we wanted to make something on our page interactive: to add a button or a toggle or a dropdown. That would lead us to JavaScript, the most widespread programming language in the world, and the only one that runs right within our web browsers.

---
<!-- .slide: class="notcenter" -->
## jQuery

???

But even in 2017 JavaScript can be confusing, so we turn to libraries like jQuery that simplify common tasks.

jQuery filled, and still fills, a critical role in the web development community.

Just because a tool isn't brand new doesn't make it obsolete: In a workshop it's the well-worn tools we trust the most.

---
<!-- .slide: class="notcenter" -->
## Data Modeling

???

Then we'll reach a point where you want to store some new type of data in WordPress.

I've seen everything from foursquare checkins to ecommerce products, to health clinic efficiency metrics stored in the WordPress database:

We model this data by defining custom post types.

Somebody at our local WordPress meetup shows us how to do it. And soon we're making our own WordPress plugins.

Our friends from the meetup encourage us to share what we've learned, and we give our first talk.

---
<!-- .slide: class="notcenter" -->

## Backbone

???

Then we want to make the interfaces for viewing our custom data bigger, but our JS files start to get unwieldy; so we follow the lead of WordPress core and start to learn JavaScript frameworks like Backbone.

These tools structure our code and give us a more powerful toolset to build our interfaces.

And on a global level that's a fairly niche skill, so we find ourselves teaching our communities how to use these tools.

We share what we've learned. People tell us how much the resources we create, the talks we give, help them on their own journey.

---
<!-- .slide: class="notcenter" -->

## REST APIs

???

And when WordPress 4.7 is released in 2016, now all data we would want to display in our new interfaces can be accessed through a modern REST API.

Somewhere along the way we realized that we've become a web application developer. It happens step by step as we make small steps to improve our websites.

---
<!-- .slide: class="notcenter" -->

![WordPress Logo](../../2014/wcsf-node-wp/images/wordpress-logo-simplified-rgb.png)

???

And this can all happen without leaving the WordPress ecosystem.

Now, It's good to try out other platforms and tools, but it is still _absolutely extraordinary_ that so much _is_ possible all within WordPress.

I know of no other product like that, especially one that isn't designed for developers.

---
<!-- .slide: class="notcenter" -->

### React <span class="fragment">&bull; Vue</span> <span class="fragment">&bull; SCSS</span> <span class="fragment">&bull; Stylus</span> <span class="fragment"><br>Node.js</span> <span class="fragment"> &bull; Webpack</span> <span class="fragment">&bull; Babel</span> <span class="fragment">&bull; Redux</span> <span class="fragment"><br>Testing</span> <span class="fragment">&bull; Performance</span> <span class="fragment">&bull; Accessibility</span> <span class="fragment"><br>Data Visualization</span> <span class="fragment">&bull; Consulting</span> <span class="fragment"><br>Teaching <span style="visibility:hidden;">&bull; Speaking</span></span>

???

And all those other things you hear about, all those other tools? Check them out. Use them in your plugins. All of these things can be made to work with WordPress.

Because it's all just code, all the way down

and code can be read, and eventually, understood

All the complexity of software development, it's all just individual tools that humans wrote to get things done.

We learn, we grow. We find the tools that work for us, and share them with others. We help each other make these tools better.

---
<!-- .slide: class="notcenter" -->

### React &bull; Vue &bull; SCSS &bull; Stylus <br>Node.js &bull; Webpack &bull; Babel &bull; Redux <br>Testing &bull; Performance &bull; Accessibility <br>Data Visualization &bull; Consulting <br>Teaching &bull; Speaking

???

And as we learn these things, some day maybe we find ourselves on this stage, in front of all of you.

I care about this learning path because I wouldn't be standing up here without WordPress. I have learned so much about programming, event organizing and speaking from being a part of my local WordPress meetup down in Boston.

WordPress took me from an unemployed recent grad, to become a leader within one of the best software communities in the world. Learning bit by bit. One step at a time.

---
<!-- .slide: class="notcenter" -->
## WordPress
#### _is for_
## Learners

???

And while this was my story, I'm not unique.

WordPress is for learners.

Whether we're developers, or business owners, or designers, photographers, podcasters, bloggers -- WordPress is a global community that supports us all.

I know many of you have followed a similar path.

And we need to make sure that we keep that path open.

---
<!-- .slide: class="notcenter" -->

# Building _a_ Learning Community

???

How do we do that? What makes WordPress a learning community?

We've already established the first principle: WordCamps and meetups are for WordPress users of all types, from writers to developers. Keeping everybody in the same room and same group keeps us honest.

---
<!-- .slide: class="notcenter" -->

# Celebrate Diversity

???

I'd say the single most important thing we can do for our community is to keep it open, and diverse.

WordPress is used around the world. We must strive to make the tools and communities we create as welcoming and open to people of different backgrounds and nations as we can.

---
<!-- .slide: class="notcenter" -->

# Prioritize Accessibility

???

In tandem with that, we should always strive to make our work accessible, so that as many people can benefit from it as possible.

---
<!-- .slide: class="notcenter" -->

# Be Kind

???

And maintaining diversity is hard, so we must also protect our community from hate & arrogance. This whole system only works if people feel comfortable entering the group, and feel safe asking for help.

---
<!-- .slide: data-background="url('./images/norcross-loopconf-talk.png')" data-state="solid-bg" data-background-position="bottom" data-background-repeat="no-repeat" data-background-size="cover" -->

[Watch on YouTube](https://www.youtube.com/watch?v=lHWI75nKWb0)
<!-- .element class="whitebg" -->

???

On that note I'd like to plug Andrew Norcross' talk from February's LoopConf event. There's a lot of nastiness on the web, and that does extend onto our own forums.

Racism. Sexism. Ableism. Xenophobia.

Resisting these things is hard. It's a community responsibility. This was a very hard talk to watch, but it's important to remember how much effort it takes to keep our community healthy.

---
<!-- .slide: class="notcenter" -->
# Learn, Share

???

But thankfully WordPress on the whole is still a healthy community, and a healthy community is a sharing community. When you learn how to do something, share it. However simple. Somebody out there won't have learned it yet.

I spend my days working with the latest versions of the most modern web libraries and tools; my colleagues are involved in designing the JavaScript programming language itself. But it's my talks on jQuery and Backbone that consistently get the most traffic. Somebody new is always looking to learn, and none of us start at the top.

---
<!-- .slide: class="notcenter" -->
## WordPress
#### _is for_
## Learners

???

Just as I know no other open source project with a community that so richly combines authors, writers, bloggers, and developers,

No other modern software product so actively encourages the full range of customization and extension, from adding a line of custom CSS through the admin all the way to creating a single-page webapp backed by a REST API.

WordPress is for learners because WordPress enables learners of all kinds.

---
<!-- .slide: data-background-video="./images/glitch-intro-video.mp4" data-state="solid-bg" data-background-position="center" data-background-repeat="no-repeat" data-background-video-loop="true" data-background-size="contain" -->
[Glitch.com](https://glitch.com)
<!-- .element: class="whitebg" -->

???

And just as we recently added the CSS editor, can take inspiration from kindred spirits in the web community about how we can build tools to inspire and reward curiosity.

This is Glitch, the product my friend Jenn Schiffer works on with Anil Dash. Glitch is a remixing platform for web programs, designed for learners.

If you see something you like, you can remix it and adjust it. No "forking," which is an awful choice of word; no command line, no editors to install. Just code, without the magic.

You can use it to make a blog, or a game, or a chat bot.

And I think we should be learning from this. Our plugins should make it easier to adjust their settings; our themes should be more open to modular remixing. We cannot restrict exploration, or WordPress loses its main advantage over Squarespace, Wix and the like.

---
<!-- .slide: class="notcenter" -->

> The power to understand and predict the quantities of the world should not be restricted to those with a freakish knack for manipulating abstract symbols.

<small><em>~ Brett Victor, [Kill Math](http://worrydream.com/KillMath/)</em></small>

???

Again, it isn't about making everybody learn to code. It's about understanding that none of this is impossible if you want to learn. And it's about keeping the doors to learning open for those of us that want to walk through them.

Nobody becomes a programmer all at once. It takes many, many steps, and every step along the way is a role and a job and a responsibility all of its own.

I have a lot left to learn. We all do.

---
<!-- .slide: class="notcenter" -->

## Encourage Curiosity

???

Because if we are kind to each other, and keep making it easier to engage in our communities and modify our software however we want, to follow our curiosity wherever it may lead,

then our community will grow as more and more people find ways to learn from the web, from WordPress, from us, and from each other.

---
<!-- .slide: class="notcenter" -->

# Democratize Software

???

If we do all these things,

then, I think, we will be democratizing software.

---
<!-- .slide: class="notcenter" -->

## Thank You

<hr>

[talks.kadamwhite.com/democratizing-software](http://talks.kadamwhite.com/democratizing-software)

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Bocoup](https://bocoup.com)

???

Thank you

---

### The Four Freedoms of Open Source:
## Use, Study, Share, and Improve
### Open-Source Software

???

This is how Open Source is meant to work. Adapting Roosevelt's idea of the four freedoms, the free software movement has defined the four freedoms of open source as the freedom to use, study, improve and to share the software.

We usually focus on the part where it says it's free to use; that's very appealing.

We also focus on our ability to come together to improve the software, and we share those improvements with one another.

But it's the ability we have to study the software,