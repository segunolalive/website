---
layout: layouts/post.njk
title: Understanding Accessibility And Assistive Technologies
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

It behaves like a similarly labelled native checkbox. It has similar mouse and keyboard interactions by default. A screen reader recognises it as identical to a native checkbox? A switch knows how to interact with it by default. What makes this possible?

## The Accessibility APIs

The accessibility frameworks and APIs mentioned earlier make all these possible. When we visit a webpage, the browser generates an Accessibility Object Model (AOM), much like the the DOM but for accessibility information. The browser sends the accessibility information to the operating system's accessibility framework using the aforementioned APIs. When we use assistive technologies like a screen reader, they query that information from the underlying framework or the browser's AOM. This is how they learn about each element, their current state, and how to interact with them.



## Semantic HTML and ARIA-*