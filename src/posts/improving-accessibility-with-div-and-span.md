---
layout: layouts/post.njk
title: Improving Accessibility With DIV and SPAN
date: 2020-05-11T16:12:39.249Z
tags:
  - accessibility
  - a11y
  - musings
---
There are nearly 150 HTML elements. Only 2 have no semantic meaning. Guess which ones? The DIV and SPAN elements. They are the only HTML elements that convey absolutely no meaning. Surprising, they're the most used elements. Are developers trying to not communicate any meaning?

In an attempt to improve accessibility, many developers demonise the div and span. They abandon the `DIV` for the `SECTION`. While that is good, I have seen many people wrap content in multiple `SECTION` elements, hence losing the semantic benefit of the `SECTION`.

Sometimes, however, what you need is an element that has no meaning. An element that says nothing. That's where you use the DIV or the SPAN. When does one need these, you ask? Every time you add an element just so you can achieve some layout or styling. That's their purpose and using them like this can actually improve your site's accessibility. Yes, I said it. Using a DIV or SPAN can improve accessibility. 

```
<section>
    <h3>Section Title</h3>
    <section class="fancy-css-class">
      <section class="some-css-class">
         Some Content wrapped within multiple section elements.
       </section>
      </section>
     ...
</section>
```

In an attempt to get rid of DIVs, and improve accessibility, I've seen devs write code like the one above. Most screen readers would ignore the inner section elements because they lack an accessible name, but some would announce the text as *"section section section Some content ..."*. Now that's just confusing and degrades the user experience. Also, reading tools like [Instapaper](https://www.instapaper.com) use HTML semantics to determine the relationship between different parts of a webpage and present content appropriately. The code above might be considered to be lower down in hierarchy – subsection of a subsection.

The  inner `sections elements`, in this case, exist simply for styling. They're wrappers but we've introduced elements with meaning. Semantic HTML defines a contract with the machines that will display our content. In this case, we've slipped some wrong terms and conditions into the contract. The inner `section` elements should be DIVs here. That way, they get ignored in the accessibility tree and the content is treated like content of the parent `section element`. 

The DIV and SPAN elements got a bad wrap for good reason – they were abused. Now, we're abusing and misusing semantic elements. If a piece of text needs to be contextually emphasized, it's tempting to wrap it in a `SPAN` and emphasize purely in CSS. However, we have the `em` and `strong` elements for that. Style appropriately after structurally communicating intent. Don't divide your page into regions using DIVs. You have landmarks e.g header, footer, main, nav for that

## When to use a DIV or SPAN

Use these elements when you intend to communicate nothing e.g you need a wrapper for styling but it doesn't affect the meaning of the content. Use the `DIV` when you need a block-level wrapper and the `SPAN` for inline wrapping.

Don't use them for anything clickable. That's already meaningful – that's already a contract/behaviour. Yes, I'm looking at you wrapping an icon in a `SPAN` and adding a click handler – yes, you. That's a button.

> Remember, communicate meaning via HTML.

Happy hacking 😉