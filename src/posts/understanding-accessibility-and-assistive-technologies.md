---
layout: layouts/post.njk
title: How Web Accessibility Works
metaDesc: A quick introduction to the inner workings of web accessibility.
socialImage: /images/a11y.png
date: 2020-06-03T09:56:42.301Z
tags:
  - accessibility
  - a11y
  - assistive technology
---
When we write HTML, the HTML tags don't run in the browser. The browser creates a tree representation of the HTML document given to it. This tree is called the Document Object Model *(DOM)*. This is what the browser translates to elements on the screen. HTML is just a declarative DSL *(Domain Specific Language)* for expressing the DOM. If you are familiar with React, it's like `JSX` being compiled to React Elements. Similarly, our CSS rules are merged with the user agent's default styles to generate the CSS Object Model *(CSSOM)*.

The DOM and CSSOM are responsible for what is rendered on the screen. This is all we need to provide information on the web to most users without any debilitating impairments. However, one-sixth of human population suffers at least one form of disability and many of them require assistive technologies to use the web. How do they get in on the action?

## Accessibility Object Model (AOM)

Just as browsers generate the DOM and CSSOM, they also generate an Accessibility Object Model. The AOM is a tree data structure similar to the Document Object Model (DOM) but for accessibility information. It is a representation of each element on the screen and their accessibility-related attributes like "name" "title", "alt", "aria-*", text content etc. This tree often corresponds closely to the representation in an operating system's Accessibility Framework.

Every mainstream operating system has built-in accessibility frameworks and APIs. For example, on the MacOs there is the [NSAccessibility Protocol](https://developer.apple.com/documentation/appkit/nsaccessibilityprotocol), Windows has [UI Automation](https://docs.microsoft.com/en-us/windows/win32/winauto/entry-uiauto-win32) to mention a few. 

These frameworks specify the behaviours of common UI widgets and patterns. The native development kits for these operating systems provide primitives that interface with these Accessibility APIs ensuring that application UIs are accessible by default. For example, here is the [checkbox class](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.checkbox?view=netcore-3.1) for `System.Windows.Forms` in dotnet core, which defines the behaviour and appearance of a native checkbox on the Windows Operating System.

On the web, we also native accessibility primitives e.g the following code block creates a checkbox with accessible name of "I accept terms". 

```html
<label for="accept-terms">I accept terms</label>
<input type="checkbox" id="accept-terms" />
```

It'll be announced as "I accept terms, unchecked checkbox" or something similar depending on the screen reader. Then the screen reader would proceed to announce the means of interaction e.g key combinations or gestures to check the box. 

It behaves like a similarly labelled native checkbox. It has similar mouse and keyboard interactions by default. A screen reader recognises it as identical to a native checkbox. A switch knows how to interact with it by default. What makes this possible? The accessibility frameworks and APIs mentioned earlier make all these possible. When we visit a webpage, the browser generates an AOM, much like the the DOM but for accessibility information. The browser can send this accessibility information to the operating system's accessibility framework using the aforementioned APIs. When we use assistive technologies like a screen reader, they query that information from the underlying framework or the browser's AOM. This is how they learn about each element, their current state, and how to interact with them.

## Semantic HTML and  Accessible Rich Internet Applications (ARIA)

Building websites using semantic HTML is the web equivalent of building a desktop or mobile app using the platform's primitive. These primitives provide a lot of information and behaviour out of the box. This information is relayed to the AOM and the platform's accessibility framework. For example, representing a clickable UI element with an HTML button says, its clickable/tappable, focusable, its function is a button, that is, clicking it does something. An assistive technology like a switch or screen reader can then query this information and relay it to a user. Of course the static nature of HTML puts some limits to its effectiveness in representing all the possible accessibility information, this is why we have ARIA attributes.

We can compose multiple HTML elements into more complex UI widgets and tie them up with scripting. For example, with some scripting, an input field can be composed with an unordered list of items to make an autocomplete widget. While this is possible, we still still need a way to tell the AOM that these elements are indeed one composite widget not just an input field and a list. This is where ARIA-roles can help. Setting a role of **combobox** on the container of the input element and **listbox** on the unordered represents the widget as a combobox and a screen reader will announce it as such. We still need some other ARIA directives such as aria-controls, aria-live etc, but those details are beyond the scope of this article.

## Custom UI Widgets

When designing or building custom UI widgets, it's important that we consider the accessibility implications of the design. It can be tempting to roll out your own solution in code but before doing so, ask: 

> Can this design be adequately represented by established UI patterns and widgets? Does that UI pattern exist in the wild?

If the answers are "yes", then there's probably a set of implementation guidelines for it already. You should follow them. These guidelines include the expected interactions, roles, and associations. Following these patterns means your users don't have to learn how to use your app, it'll work just like any other application on their operating system. Also, you wont have to provide instructions for all the different assistive technologies your users could be using. A good place to get started is the [W3C WAI ARIA PRACTICES](https://www.w3.org/TR/wai-aria-practices/)

## Summary

There are standardised ways of representing UI elements such that they work well for all users. These standards are mostly uniformly implemented across platforms and operating systems and exposed as platform Accessibility APIs. Assistive technologies depend on these APIs to accurately represent the UI to users as well as help them interact with it. Browsers also provide an Accessibility Object Model that assistive technologies can query.

*Post Script*: There is ongoing work to allow web developers query the AOM in future, although there are concerns about privacy and possible discriminatory usage of such information.