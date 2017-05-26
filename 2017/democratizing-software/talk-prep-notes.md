# WCEU Datavis talk

> With WordPress 4.7 we gained REST API endpoints for core data types—now what can we do with them? We’re seeing how the REST API is being used to build new and better editing interfaces, but we also have a huge opportunity to use that API to explore the data we already have within our sites. It’s never been so easy to access our WordPress content from JavaScript, so let’s see what we can learn about it through data visualization!
>
> I will share how we can combine the REST API with visualization tools like D3.js to gain new insights into your content. We will build a network diagram to visualize how tags and categories area applied to posts, then discover how to use custom post types and register_meta to build a completely custom dashboard within WordPress for any type of data.

Intro options:

- Story of WP is to some extent story of staying abreast of outside developments, and folding them back in (Backbone, WP API)
- Elections: everybody spending more time looking at charts than usual (german, french, us)
- Jetpack stats vis

## Outline

- Data Visualization. It is a broad term that covers many sorts of graphics we are used to seeing on a daily basis.
    + News charts
        * Election stuff? yuck
    + Analytics
        * https://wordpress.com/stats/insights/www.kadamwhite.com
        * https://analytics.google.com/analytics/web/
- Also one of our specialties at Bocoup. Been doing large-scale data analysis (MLab), dashboards & analysis tools, and building research software
    + http://www.chicagomag.com/city-life/January-2017/Obama-Farewell-Speech/
    + https://bocoup.com/services/datavis
    + http://viz.measurementlab.net/location/eufra8paris?isps=AS12322_AS3215_AS21502
    + https://bocoup.com/work/cancer-browser
- But when I talk to WP folks, there's a sense that these tools and techniques are less applicable to us, for some reason
    + We get our analytics from external providers like Google or Jetpack/Automattic, e.g.
    + Or that the content we're working with isn't relevant to data visualization, or vice-versa
- But taking the example of news graphics: WordPress is often used for news, and interactive graphics could really enhance our articles.
    + We do this at Bocoup to illustrate our tools
        * https://bocoup.com/blog/smoothly-animate-thousands-of-points-with-html5-canvas-and-d3
- Looking at analytics, many of our plugins provide interesting information that we could do a better job of depicting visually in the admin dashboard
- And perhaps most interestingly, we store the very words we press in a database -- content is data, too. What could we do to visualize the content or editorial metadata in our wp posts tables?
- So, the purpose of this talk is to de-mystify data visualization.
- It is not a code talk, but it will explain loosely how different dimensions of data can be translated into visuals
    + and will point the way to code samples and resources where appropriate

WHAT SHOULD FIRST EXAMPLE BE?

- Pulling in Swarm RSS for checkin map?
- Github-style post contributions graph
- Post periodicity spiral
- Tag force-directed graph
- DATA MODELING: what's a good data type

Resources

- Data Sketches
