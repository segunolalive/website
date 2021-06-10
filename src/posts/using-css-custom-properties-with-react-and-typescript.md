---
layout: layouts/post.njk
title: Using CSS Custom Properties With React And Typescript
date: 2021-06-10T08:23:52.081Z
---
Sometimes, we want to update UI styles based on some dynamic variable. In React world, that would be a component prop, state or value from a context provider. This is one of the arguments for reaching out for a CSS in JS solution like emotion. However, CSS has native support for variables that change at runtime. The "official" term for these variables is custom properties.



*Type '{ '--height': number; }' is not assignable to type 'CSSProperties'.
  Object literal may only specify known properties, and ''--height'' does not exist in type 'CSSProperties'.*