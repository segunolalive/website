---
layout: layouts/post.njk
title: Avoid Giving Screen Reader Hints
date: 2020-06-03T10:12:33.737Z
tags:
  - accessibility
  - "#a11y"
---
Recently, a colleague asked to add hints for screen readers on a custom UI widget we had worked on together but I refused. Why?

## Background

For context, the widget in question is a tab list. We built it following the standard requirements, making sure to add the appropriate roles, and handling mouse and keyboard interactions. This means users can cycle through the tabs using the left/right arrow keys and they can select a desired tab using the enter or space key. They can focus send focus to the tab panel using the tab key. Pressing the left/right arrow keys while focus is within a tab panel still cycles through the tabs. This is all pretty standard.

In our case, the tab panels contained many interactive elements and the team was concerned that screen reader users might focus on the contents of the first tab panel without knowing how to navigate to other tabs/tab panels. This seems like reasonable concern, especially if you're not used to navigating the web using screen readers. However, when a screen reader encounters a tab list, it announces it like this: