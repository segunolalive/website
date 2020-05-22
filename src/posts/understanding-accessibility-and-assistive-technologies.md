---
layout: layouts/post.njk
title: Accessibility, Web Accessibility And Assistive Technologies
metaDesc: Learn how web accessibility works under the hood, how you can apply it
  and avoid pitfalls when building software.
date: 2020-05-19T06:53:19.657Z
tags:
  - accessibility
  - a11y
  - musings
---
Every mainstream operating system has built-in accessibility frameworks and APIs. On MacOs, we have the [NSAccessibility Protocol](https://developer.apple.com/documentation/appkit/nsaccessibilityprotocol). On Windows, we have [UI Automation](https://docs.microsoft.com/en-us/windows/win32/winauto/entry-uiauto-win32). These frameworks specify the behaviours of common UI widgets and patterns. The native development frameworks for these operating systems provide primitives that interface with these Accessibility APIs ensuring that application UIs are accessible by default. For example, here is the [checkbox class](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.checkbox?view=netcore-3.1) for `System.Windows.Forms` in dotnet core, which defines the behaviour and appearance of a native checkbox on the Windows Operating System.

On the web, we also native accessibility primitives e.g the following creates a checkbox with accessible name of "I accept terms". It'll be announced as "I accept terms, unchecked checkbox" or something similar depending on the screen reader. Then the screen reader would proceed to announce the keyboard actions required to check the box. 

```html
<label for="accept-terms">I accept terms</label>
<input type="checkbox" id="accept-terms" />
```

It behaves like a similarly labelled native checkbox. It has similar mouse and keyboard interactions by default. A screen reader recognises it as identical to a native checkbox. A switch knows how to interact with it by default. What makes this possible? The accessibility frameworks and APIs mentioned earlier make all these possible. When we visit a webpage, the browser generates an Accessibility Object Model (AOM), much like the the DOM but for accessibility information. The browser sends the accessibility information to the operating system's accessibility framework using the aforementioned APIs. When we use assistive technologies like a screen reader, they query that information from the underlying framework or the browser's AOM. This is how they learn about each element, their current state, and how to interact with them.

## Accessibility Object Model (AOM)

The AOM is a tree data structure similar to the Document Object Model (DOM) but for accessibility information. It is a representation of each element on a page and their accessibility-related attributes like "title", "alt", "aria-*", text content etc. This tree often corresponds nicely to the representation in an operating system's Accessibility Framework.

## Semantic HTML and  Accessible Rich Internet Applications (ARIA)

Building websites using semantic HTML is the web equivalent of building a desktop or mobile app using the platform's primitive. These primitives provide a lot of information and behaviour out of the box. This information is relayed to the AOM and the platform's accessibility framework. For example, representing a clickable UI element with an HTML button says, its clickable/tappable, focusable, its function is a button – clicking it does something. An assistive technology like a switch or screen reader can then query this information and relay it to a user. Of course the static nature of HTML puts some limits to its effectiveness in representing all the possible accessibility information, so we have ARIA attributes.

We can compose multiple HTML elements into more complex UI widgets and tie them up with scripting. For example, with some scripting, an input field can be composed with an unordered list of items to make an autocomplete widget. While this is possible, we still still need a way to tell the AOM that these elements are indeed one composite widget not just an input field and a list. This is where ARIA-roles can help. Setting a role of **combobox** on the container of the input element and **listbox** on the unordered represents the widget as a combobox and a screen reader will announce it as such. We still need some other ARIA directives such as aria-controls etc, but those details are beyond the scope of this article.



## Custom UI Widgets

When designing or building custom UI widgets, it's important that we consider the accessibility implications of the design. It can be tempting to roll out your own solution in code but before doing so ask: "can this design be adequately represented by established UI patterns and widgets? Does that UI pattern exist in the wild?" If the answers are "yes", then there's probably a set of implementation guidelines for it already. You should follow them. These guidelines include the expected interactions, roles, and associations. Following these patterns means your users don't have to learn how to use your app, it'll work just like any other application on their operating system. Also, you wont have to provide instructions for all the different assistive technologies your users could be using.