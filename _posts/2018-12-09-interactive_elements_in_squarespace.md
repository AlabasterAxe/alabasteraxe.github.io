---
id: 20
timestamp: 1544376495
author: "Matt Keller"
title: "Using Angular Elements to create interactive blog posts on Squarespace"
excerpt: "Sometimes Squarespaces' WYSIWYG editor can feel a bit restrictive, but Angular Elements provide a way to spice things up a bit."
---

One of the goals of this blog is to break down and illustrate complex topics through visualisations, (see the [precedence series](https://www.thkp.co/blog?tag=precedence) and the [great algorithms series](https://www.thkp.co/blog?tag=great%20algorithms)). To take it a step further, I wanted to add interactive examples that would illustrate the concept, building up the complexity as the reader progressed. (I derived much inspiration from the format of the fantastic [parable of the polygons](https://ncase.me/polygons/)).

Adding a bit of complexity to the task is that our blog is hosted with Squarespace. While Squarespace allows a lot of freedom, this definitely introduced some challenges that I needed to work around. Read on for a walk-through of my solution!

## The Goal

Roughly speaking, I wanted to write a blog post that followed this layout:

![20181204_015809.png](https://images.squarespace-cdn.com/content/v1/5bc3ae2ca56827a279bf229b/1544109097777-QIFUMYX672GE9CXKKJZ6/20181204_015809.png?format=1500w)

So each section of the post would have a corresponding demo to drive home its intended point.

The structure of each demo was straight-forward. It had an HTML canvas for drawing the interactive diagrams and a couple of html sliders that controlled the demo:

![SmartSelect_20181206-164558_Onshape.jpg](https://images.squarespace-cdn.com/content/v1/5bc3ae2ca56827a279bf229b/1544111292408-E6IQHH15IJK5H63AAQYC/SmartSelect_20181206-164558_Onshape.jpg?format=1500w)

Ultimately, each demo would have a few html elements and some javascript used to wire things together and draw the canvas.

Squarespace provides the ability to add custom snippets of html and JavaScript. In theory, I could have just written all of the code directly into Squarespace’s editor but I wanted to implement this in such a way that wouldn’t require me to repeatedly copy paste javascript and html code as I updated the demo. That seemed like it would tedious and error prone.

# Angular to the rescue

Having worked with Angular before, my first thought was to create a component to encapsulate the html template and JavaScript (TypeScript, technically since that's the language, Angular uses). So that’s what I did. I wrote an Angular component that had a couple of sliders and a canvas, and my component class which responded to input change events and made the corresponding updates to the canvas.

  
(If you're new to Angular, and interested in learning more, I recommend going through [the official intro tutorial](https://angular.io/tutorial))

![angular.png](https://images.squarespace-cdn.com/content/v1/5bc3ae2ca56827a279bf229b/1543785119114-BCSBEARWZ7SKOGCQWHM2/angular.png?format=500w)

I made the component configurable so that the same component could be used for every step just with a different configuration.

Boom. Problem solved, right? Not exactly.

Angular components define a handle by which they can be referenced. For example, if I have a component that declares itself as ‘demo-widget’, other components can reference it by adding <demo-widget></demo-widget> in their template.

Even though I had my Angular component, if I tried to reference it in my blog post in an HTML snippet, the browser wouldn't recognize it. By default, Angular components can only be referenced from other components’ templates.

I needed a way to reference my Angular component outside of an Angular App.

## Enter Angular Elements

Early in 2018, the Angular team released [Angular Elements](https://angular.io/guide/elements) which allows you to turn your Angular components into [custom HTML Elements](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements) which you can reference from vanilla HTML (or another framework, for that matter, e.g. returning this from a React render method or reference this from a Django template) once you import the JS code for your component.

(I won’t go into all of the details about how to set Angular Elements up here but I found [Nitay Neeman's Blog post](https://nitayneeman.com/posts/a-practical-guide-to-angular-elements/) a very useful addendum to the official docs.)

Perfect, this was pretty much a drop in solution for my problem.

## Putting it all together

Awesome, so that’s all the different building blocks. I had a reusable component that I could integrate into my non-Angular environment. Now the only thing left was to wire it all together.

### BUILD AND SERVE THE ANGULAR COMPONENT

Once I was done developing the component I needed to build it and put it somewhere that your Squarespace site could access it from. I put mine into a public bucket on AWS S3

### IMPORT THE JS

As mentioned above, Squarespace has a code widget that allows you to write custom JS, HTML or CSS. So at the top of the blog post I added some <script> tags that reference the component’s compiled JS code.

### ADD THE CUSTOM ELEMENTS

Now that the post was fetching the js sources for the Angular element, I added the custom element wherever the blog post needed the demo with additional code widgets.

## Conclusion

So this was a quick, high-level summary of an approach that worked for me when I was looking to build an interactive blog post on Squarespace. There are definitely alternative approaches that would probably also have worked (off the top of my head, Polymer Web Components seem like they might have been a more natural fit but I just wasn’t familiar with how to do that ¯\_(ツ)_/¯) In addition, there are also clear areas for improvement:

-   Slow build / deploy process
    
    -   Putting some automation in place to push the code to the static content server (s3 in my case) would allow tighter cycles.
        
-   S3 Caching issues
    
    -   For whatever reason, the versions of the JS served from S3 was always stale so I needed to do manual cache busting by uploading a newly named directory to S3
        

Overall, I’m pretty happy with how things turned out (check out the final result [here](https://www.thkp.co/blog/2018/11/19/ml-chapter-2-a-closer-look-at-loss-with-linear-regression)) and I’m planning on using this initial work to build even more ambitious blog posts in the future!