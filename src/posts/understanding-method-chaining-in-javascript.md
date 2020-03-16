---
layout: layouts/post.njk
title: Understanding Method Chaining In Javascript
metaTitle: Understanding Method Chaining In Javascript
metaDesc: ' When programming, it is commonplace to have actions that need to run in a defined series of steps. In this article, Segun explains how to write code that is chainable and easier to read.'
socialImage: images/0-wx-3njkwp88hrlkx.jpeg
date: 2018-12-06T10:43:19.236Z
tags:
  - js
---
![Chain by Kaley Dykstra from Unsplash](/images/0-wx-3njkwp88hrlkx.jpeg)

When programming, it is commonplace to have actions that need to run in a defined series of steps. Writing a single function that defines all these actions is usually a terrible idea, so we write a number of functions/methods that deal with individual actions. To cater for this, we pass the results of the previous method as arguments to the next method. Then, we end up with something like this:

```javascript
const myObject = new ClassIWrote()

myObject.someMethod(
  myObject.someOtherMethod(
    myObject.yetAnotherMethod()
  )
)
```

*Sample code with nested function calls*

The sample code above doesn’t seem that bad or unreadable at first. It’s just a couple of nested function calls, right? No, you couldn’t be further from the truth. Take a moment to think about how data flows through these nested function calls. The code reads top-down

> first **myObject.someMethod**
>
> then **myObject.someOtherMethod**
>
> then **myObject.yetAnotherMethod**

but the flow of data is actually in the reverse direction (down-up).

> First **myObject.someMethod** 
>
> then **myObject.yetAnotherMethod**
>
> then **myObject.someOtherMethod**        

Worst of all, we actually have to intentionally craft the code in the reverse order — write the last function first, then pass it the function whose return value it depends on and so on till we get to the first function in the chain. Now, what happens to the code’s readability when our pipeline of functions gets even longer? For example, when we have ten functions, our code would take on a triangular shape like our best friend from wayback, the [callback hell](http://callbackhell.com/).

![Callback Hell from \[http://blog.mclain.ca/\](http://blog.mclain.ca/)](https://cdn-images-1.medium.com/max/3544/1*s-OlfkC2Y1zg9m8S4rUlWQ.png)*Callback Hell from <http://blog.mclain.ca/>*

However, if you’ve ever used a library like jQuery, you must have written or seen code like this:

![](https://cdn-images-1.medium.com/max/2616/1*G2oxKcQMtEjoO-WzoCXnnw.png)

Isn’t this clean and readable? If we chained ten functions together, it’ll still read nicely, top-down. No train of trailing parentheses and semi-colons — God help you if you mistakingly leave one of them out or add an extra one in the wrong place. Best of all, this code reads in the same direction as the data flow. Won't it be nice if our code read the same? So, how do we go from our initial abomination of unreadable junk of nested functions to the clean and beautiful chain of easily readable and understandable code shown above?

## It’s all about THIS

In Javascript, this refers to the current object instance. Unlike most mainstream programming languages, Javascript’s this depends on how and where a method/function is called. If that last statement went over your head, just ignore it. You are not alone. this is a common cause of misunderstanding in Javascript.

<blockquote class="twitter-tweet" data-theme="light"><p lang="en" dir="ltr">Sometimes when I&#39;m writing Javascript I want to throw up my hands and say &quot;this is bullshit!&quot; but I can never remember what &quot;this&quot; refers to</p>&mdash; Ben Halpern 🦁 (@bendhalpern) <a href="https://twitter.com/bendhalpern/status/578925947245633536?ref_src=twsrc%5Etfw">March 20, 2015</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

We won’t be going into the intricacies of Javascript's this in this article. There are tons of amazing resources that explain how this works in detail. A good place to start is the Mozilla Developers Network ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)). I just thought to introduce it because it holds the key to chaining methods. However, for the sake of this article, when we create an object using an expression such as `object = new SomeClassWeCreated()`, and call the methods defined on that object, this refers to that object. There’s more to this than this. All pun intended.

As mentioned earlier, this is the current object instance, therefore, it has access to all the methods defined on the instance as well as access to the [prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype). So, if we wanted to access a method defined on the current object instance (which this refers to), we can write `this.someMethod()`. Cool, yeah?

Next step is to find a way to make sure that we can call another method on the return value of the this.someMethod(), so we can have this.someMethod().someOtherMethod(). To achieve this, we simply tell our methods to return this. That way, each method returns the object that contains the methods we want.

<iframe src="https://medium.com/media/ec7ff1d5f4610dd1afbac5092dce0e02" frameborder=0></iframe>

Okay, that’s all nice and good. Now we can chain our methods and produce some side-effects — logging to the console in this case. Our code is a lot more readable and clean, but how do we get actual values from our chainable class?

## Instance Properties

To get the result of our chain of function calls, we need to store the results of each function call and then access that data at the end of our chain. For this, we’ll add an instance property to our class to hold the result of each function/method call.

Instance properties are properties unique to each object instance, meaning if we create two objects(instances) from the same class by writing new SomeClassWeWrote(), their values can be manipulated independently. Since this refers to the current object instance, attaching the property to this e.g this.property = ‘someValue' guarantees it’ll be available to the current instance and not shared with other instances of the same class.

<iframe src="https://medium.com/media/3aecadaea5570dc58193c105e360cd67" frameborder=0></iframe>

Let’s run through the code.

This example shares lots of similarities with the ChainAble class shown before. It contains methods that do some things, then return this. However, instead of just logging to the console, they store the results of their computations in an instance variable, this.value. In order to access the result of our computations, we add .value at the end of our chain of method calls.

## Getting Values With Getters

Because I like the idea, I have decided to slip in something extra. Instead of accessing our value directly, we could define a getter that lets us *get* our value. This is done by defining a dedicated function prefixed with get between lines **3 and 5** which has the responsibility of returning the final result. Then we access it like a regular property on line **15**.

<iframe src="https://medium.com/media/c49c4a41bc19102c5c5438fd85b4ff28" frameborder=0></iframe>

On that note, we have successfully created a class with chainable methods as well as a dedicated *public* API for accessing the result of our computations. This is the final code for our *Arithmetic* class:

<iframe src="https://medium.com/media/f11d50496081c3e958bb299923bb1a5f" frameborder=0></iframe>

*If you liked this article or learned something from it, do give a round of applause and help share with your network. Thank you.*