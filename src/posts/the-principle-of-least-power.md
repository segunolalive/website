---
layout: layouts/post.njk
title: The Principle of Least Power
metaTitle: The Principle of Least Power
socialImage: images/joanna-kosinska-laasol0lrys-unsplash.jpg
date: 2020-03-16T08:36:52.801Z
tags:
  - css
  - html
  - js
---
A few weeks ago, I saw a tweet that contained the phrase “*principle of least power” .* It represents the idea of solving a problem using as minimal arsenal from your toolset as necessary. For example, not using javascript for things that are easily achievable with CSS.

### Why?

I have encountered a number of interesting situations where I have found that taking a moment to do a bit of research often reveals simpler alternative solutions with tools we are already pretty familiar with.

### Scenario 1

Sometime ago, I needed to display a piece of text on a web page as a superscript, so I asked a friend how he’ll do it. Without wasting a breath, he told me he’d wrap it in an html span tag, then using CSS he’ll reduce the font-size and add a vertical-align: top. Take a look at the pen below.

<iframe height="455" style="width: 100%;" scrolling="no" title="superscript with CSS" src="https://codepen.io/segunolalive/embed/oyBVgY?height=455&theme-id=dark&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/segunolalive/pen/oyBVgY'>superscript with CSS</a> by Segun Ola
  (<a href='https://codepen.io/segunolalive'>@segunolalive</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

That definitely works and is a smart way of taking advantage of span tags being inline. However, it’s unnecessary work and *smartness*. Html already provides `<sup>` tag for such. There’s also a similar `<sub>` tag for subscripts. It’s semantic. Anyone or anything reading your code knows exactly what you mean unlike the ad-hoc CSS approach.

### Scenario 2

Recently, a colleague was tasked with creating a sticky header. You know those headers that scroll along with the page until you reach a certain height where they get fixed. She was struggling to justify reaching out to an old friend, jQuery, just for this piece of functionality. She also didn’t want to deal with wiring up event listeners and cleaning up afterwards, adding and removing CSS classes etc. Did I mention it was a React project. So she’d have to convert her stateless functional component to a class component, then set up life-cycle methods. It’s not much but it definitely is too much for such a simple thing. No need to reach out to JavaScript or jQuery for something achievable with two lines of CSS.

```css
position: sticky;
top: **insert arbitrary CSS length**
```

**NB:** you could use top, bottom, left or right, depending on your use-case. Also, note that the length is calculated relative to the bounding box of the containing element. So, top above isn’t relative to the viewport but the container. Position **sticky** is the love-child of **relative** and **fixed.**

### Scenario 3

I have been working on a React project with a lot of broken image links. This has made the app ugly because it’s heavily-dependent on images. Before you say ‘*duh, fix the links*’, these are user-generated content, so I can’t simply change the links. Some are due to an AWS S3 authorisation issue that I don’t remember why we’ve refused to do anything about . Anyway, one of my teammates was like:

> “We need to fix these broken images. What can you guys on the frontend do about it?”

I was quick to explain how HTTP requests work, how browsers parse the HTML documents and how that there was nothing we could do if the request failed. We could only provide fallbacks if the user never uploaded an image using something like this:

```html
   <img src={user.image ? user.image || fallbackImage} alt="something fancy" />
```

However, I couldn’t have been more wrong. The **<img/>** tag receives an ***onerror*** attribute that you can use to provide custom behaviour and support goes far back as IE.

```html
    <img src="too-much-sauce"
      alt="image of plenty of source"
      onerror="this.onerror=null; this.src = 'some-new-url';"
    />
```

The pen below demonstrates this. The first image shows the desired image. In the second and third, I have altered the URL such that the image breaks. However, I provided an error handler that swaps the src to that of a fallback image in the third instance.

<iframe height="500" style="width: 100%;" scrolling="no" title="img tag fallback" src="https://codepen.io/segunolalive/embed/PapRvx?height=500&theme-id=dark&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/segunolalive/pen/PapRvx'>img tag fallback</a> by Segun Ola
  (<a href='https://codepen.io/segunolalive'>@segunolalive</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

Note that setting the error handler to null, `this.onerror=null`, is necessary to prevent an infinite loop in case the fallback also encounters an error.

### Other Scenarios (or *skinarios 😜)*

On another project, I’ve worked on this year, 2018 to be clear 😄, I saw layouts done with:

```css
display: table;
content: ' ';
padding: *something ridiculous*
...
and myriads to media queries to adjust the padding per screen size
```

It’s **2018!** The desired effect could easily have been achieved using Flexbox and percentages for widths.

I have seen people load up **moment.js** just to convert date to locale time or date when the following could have solved the same problem without the extra library.

```javascript
const dateOptions = {
      weekday: 'long',
      year: 'numeric',
      month: 'long',
      day: 'numeric'
};
new Date().toLocaleDateString('en-US', dateOptions) // **Monday, June 11, 2018**
```

**NB:** If you need to support older browsers, you’d need a polyfill.

This is no exhaustive list but I believe these demonstrate that there’s usually a simpler way to solve basic non-edge case problems.

Having an in-depth knowledge of your tools cannot be overstated. You might start out building cool stuff with just basic knowledge but investing to know more is often necessary.

Start small. Bring out the big guns only when necessary. Also, don’t be too quick to rush into using only what you’re familiar with.

> # If all you have is a hammer, everything begins to look like nails — Law of the Instrument (paraphrased)

*Special appreciation to [Chuks El-Gran Opia](https://twitter.com/developia_), [Temitope Joloko](https://twitter.com/temmy_jade),[ Enodi Audu](https://twitter.com/a_enodi), [Ebuka Umeh](https://twitter.com/obitojs), [Bolaji](https://twitter.com/Bolaji___), [amarachi akuwudike](https://twitter.com/aimeedykii), for helping with this article.*