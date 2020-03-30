---
layout: layouts/post.njk
title: React Hooks and Intersection Observer
metaTitle: React Hooks and Intersection Observer
date: 2020-03-29T18:45:39.961Z
tags:
  - react
  - js
  - intersection observer
---
Using the intersection observer API with React hooks is one of those instances where the fundamental differences in the React programming paradigm and the DOM become obvious. As a result of these differences, it sometimes feel like one is forcing a square peg into a triangular hole.

This is not an exposition on the Intersection Observer. You can learn more about it [here](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API). We also have some videos at [Front-End Weekly](http://frontendweekly.dev/), specifically the ones on Intersection Observer and Lazy-Loading Techniques.



```javascript
import React, { useEffect, useState, useRef } from 'react';

function doStuffOnScroll () {
  const [count, setCount] = useState(0)
  const doSomething = (entry) => {
    if (entry.isIntersecting && entry.intersectionRatio === 1) {
      setCount(count => count + 1)
    }
  }
  const spanRef = useRef()
  const spanObserver = new IntersectionObserver(doSomething)
  
  useEffect(() => {
    spanObserver.observe(spanRef)
    return () => spanObserver.disconnect()
  }, [count])
  return (
    <div>
      // ...
    <span ref={spanRef} />
    </div>
  )
}
```



You might be surprised to find that the count never increases past **1.**