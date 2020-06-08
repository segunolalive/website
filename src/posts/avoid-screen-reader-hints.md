---
layout: layouts/post.njk
title: Avoid Screen Reader Hints
date: 2020-06-04T09:41:20.084Z
tags:
  - a11y
  - accessibility
---
Recently, a colleague asked to add hints for screen readers on a custom UI widget we had worked on together but I refused. Why?

## Background

For context, the widget in question is a tab list. We built it following the standard requirements, making sure to add the appropriate roles, and handling mouse and keyboard interactions. This means users can cycle through the tabs using the left/right arrow keys and they can select a desired tab using the enter or space key. They can focus send focus to the tab panel using the tab key. Pressing the left/right arrow keys while focus is within a tab panel still cycles through the tabs. This is all pretty standard.

In our case, the tab panels contained many interactive elements and the team was concerned that screen reader users might focus on the contents of the first tab panel without knowing how to navigate to other tabs/tab panels. This seems like reasonable concern, especially if you're not used to navigating the web using screen readers. However, when a screen reader encounters a selected tab with the text "recipes", it announces it like this:

> Recipes. Selected tab, 1 of 5.

Depending on the screen reader, it might announce the keyboard combinations or gestures for selecting the current tab or navigating between the tabs and tab panels. Also, if the element with the role of `"tablist"` has an accessible name, then it might be announces as a tab group e.g _"Account Info Tab group"_. VoiceOver does this.

Also note that the screen reader announced that we're in a list. Most screen reader users already know how to navigate common UI patterns like list. They even have specialised keyboard shortcuts for quick navigation.

## Why Hints Can Be Bad
Adding keyboard hints for screen reader users tends to add noise to the user experience. Imagine users who are already familiar with navigating web content using their screen reader shortcuts having to listen through extra information that actually adds nothing to them. 

Also, they're several screen readers and they all have custom controls. Would you add instructors for every one? Some users are on mobile and touch screens, would you also include information for gestures? In the end, you'd only succeed at giving a terrible experience to all users.

## When To Use Hints
Hints aren't all bad and sometimes can be necessary but before going down that route, be sure it's the right decision.

A good use for hints is when you need to provide extra information on *non-interactive* elements e.g a carousel slide. In t
















