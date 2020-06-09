---
layout: layouts/post.njk
title: Avoid Screen Reader Hints
metaDesc: It can be tempting to provide control hints for screen readers, resist
  the urge. In this article, Segun explains why adding control hints can lead to
  a degraded experience for screen reader users.
date: 2020-06-08T13:08:33.054Z
tags:
  - a11y
  - accessibility
---
Recently, a colleague asked to add control hints for screen readers on a custom UI widget we had worked on together but I refused. Why?

## Background

For context, the widget in question is a tab list. We built it following the standard requirements, making sure to add the appropriate roles, and handling mouse and keyboard interactions. This means users can cycle through the tabs using the left/right arrow keys and they can select a desired tab using the enter or space key. They can send focus to the tab panel using the tab key. Pressing the left/right arrow keys while focus is within a tab panel still cycles through the tabs. This is all pretty standard.

In our case, the tab panels contained many interactive elements and the team was concerned that screen reader users might focus on the contents of the first tab panel without knowing how to navigate to other tabs/tab panels. This seems reasonable, especially if you're not used to navigating the web using screen readers. However, when a screen reader encounters a selected tab with the text "recipes", it announces it like this:

> Recipes. Selected tab, 1 of 5.

This tells the user that they're on a the first tab of 5 in a tab list and that the current tab is the selected tab. Depending on the screen reader, it might announce the keyboard combinations or gestures for selecting the current tab or navigating between the tabs and tab panels. Also, if the element with the role of `"tablist"` has an accessible name, then it might be announced as a tab group e.g _"Account Info Tab group"_. VoiceOver does this.

Also note that the screen reader announced that we're in a list. Most screen reader users already know how to navigate common UI patterns like lists. They even have specialised keyboard shortcuts for quick navigation.

## Why Hints Can Be Bad
Adding keyboard hints for screen reader users tends to add noise to the user experience. Imagine users who are already familiar with navigating web content using their screen reader shortcuts having to listen through extra information that actually adds nothing to them. 

Also, there are several screen readers and they all have custom controls. Would you add instructors for every single one of them? Some users are on mobile and touch screens, would you also include information for gestures? In the end, you'd only succeed at giving a terrible experience to all users.

This is why it's important to use established patterns in your User Interfaces. If you need to provide instructions to screen readers on how to interact with your UI widgets, halt, and rethink. Chances are you are doing something wrong.

For further learning, [checkout this article by Adrian Roselli](https://adrianroselli.com/2019/10/stop-giving-control-hints-to-screen-readers.html). Adrian has done the work of making videos of different screen reader/browser combinations to help demonstrate this.
















