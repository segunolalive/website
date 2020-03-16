---
layout: layouts/post.njk
title: The UX of Waiting
metaTitle: The UX of Waiting
socialImage: images/0-gupaqcsbl76nty-m.jpeg
date: 2018-11-21T17:37:49.896Z
tags:
  - UI/UX
  - musings
---
![man staring at his watch](images/0-gupaqcsbl76nty-m.jpeg "Credits: [rawpixel](https://unsplash.com/@rawpixel/collections)")



It’s 2018.

It’ll soon be 2019. Just saying. You might not have realized it 🤷‍♂ . Anyway, every website (almost) is a Single Page App (SPA) where a nearly empty page is served quickly and the user is presented with a loader to tell them “*hey, we’re not a slow site. we’re just fetching the data you need”.* This experience is often repeated when moving between pages on the app.

My congenital need for sarcasm aside, this is actually a good approach for building web apps — highly interactive websites — and I follow this approach myself. My problem, however, is with loaders. Agreed, seeing a spinner is way better UX than a blank white screen of gloom. However, that experience can quickly deteriorate depending on the loader.

This is not an article about optimizing your page size to load faster or another article bashing SPAs as abominable. I’d leave that to those who know better. This is about the fact that sometimes, you just can’t make things any faster given your constraints — poor network, some slow server-side operation etc. This is about making the waiting less painful. This is about making slow things less obvious.

> # Make the wait less painful

![Photo by \[Colter Olmstead\](https://unsplash.com/@colterolmstead?utm_source=medium&utm_medium=referral) on \[Unsplash\](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/10368/0*3WSDpL6wJDFUK9K5)*Photo by [Colter Olmstead](https://unsplash.com/@colterolmstead?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

Slow, boring or monotonous loaders/spinners make the wait seem longer. It could get so bad that it begins to feel longer than if it was a blank screen because they literally tell you “*It’s loading sooooooooooooo slowly”.* Okay, make it faster and life is good. Well, not so fast. Literally, not so fast.

Very fast loaders over-compensate and do not capture the users’ attention long enough to take their minds off the wait. Now, all your users see is fast-moving objects without context while you *waste* their time.

The waiting/loading experience should be treated as a part of the application flow because it’s more or less inevitable. It should be baked into an app’s design. Not just the color or shape of the loader but the whole experience. It should captivate the user. If possible, make the user look forward to seeing the loader.

I once worked on an app that was abysmally slow. Oh dear. I inherited the app and had to come up with ways to make it suck less. Among the optimizations made was a fast spinning loader. It wasn’t the best loader ever. Actually, it was pretty mediocre but users liked it. The secret sauce was the founder of the company asked that we replace the **loading…** text with some randomly selected cheezy notes that reflected their brand. We also made the text alternate between a transparent state and full opacity, meaning the text had to be displayed a few times for most users to read all of it. Genius! Their wait was suddenly a comedy skit and it seemed a lot shorter. I even got reports that some users intentionally reloaded the page just to see the cheezy notes.

The app still sucked and was still slow but that it sucked a little less and the wait was a bit more bearable.

I have seen a number of amazing loaders, some with sophisticated designs and animations, others simple but effective and some that are so interactive one might not consider them loaders e.g [Invsion’s Design Better](https://www.designbetter.co). My general observation has been this:

The best loaders often have multiple states, each state is often long enough (~200–400ms) to just get noticed before transitioning to the next state, leaving some desire to see it again. They often have multiple elements, not too many (3-5), undergoing the aforementioned state changes. The state transitions are fluid — the points of change are usually not too obvious, making them pleasant distractions as opposed to annoying ones.

> # The loader is itself a journey.

Taking these observations into account, I decided to build a simple loader.

![A gif of the loader I made](https://cdn-images-1.medium.com/max/2192/1*F-EgOdnudDW7L4-8Iky8FA.gif)*A gif of the loader I made*

The code for the loader is hosted on Codepen. Click the link below to see it. [Loader Pen on codepen.io](https://codepen.io/segunolalive/pen/JmVMOm)

I know it begins to feel boring after the third cycle or so but that’s after **6seconds** of waiting. At this point, your content should be loaded — hopefully. I hope that wasn’t another painful 6seconds for you. If your content isn’t loaded before the wait gets boring, you definitely should be reading those articles about page size optimization and latency reductions.

Here are even more amazing loaders to relish. You can find many more on Dribble and similar platforms.

* [SVG Tree Loader](https://codepen.io/juergengenser/pen/dPoQpY): Each iteration lasts 5 seconds.
* [CSS Stair Loader](https://codepen.io/ispal/pen/mVaaJe): Each iteration lasts 4 seconds.
* [Gear Loader](https://codepen.io/jonitrythall/pen/ojKgdx): Each iteration lasts 5 seconds.

There may be concerns about animations being distracting but that speaks more about the quality of the animations than the value of animations. Anyway, you can always have a fallback strategy with simple but well-presented text. This could be particularly useful if your user explicitly demands no animations.