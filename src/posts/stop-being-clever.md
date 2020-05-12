---
layout: layouts/post.njk
title: Stop Being Clever
metaTitle: Stop Being Clever
metaDesc: A tongue-in-cheek take on premature optimisations.
socialImage: images/0-jfrsnrquqwpg6kjc.jpeg
date: 2019-06-17T17:19:24.786Z
tags:
  - musings
---
![insert something clever](/images/0-jfrsnrquqwpg6kjc.jpeg "Credits: by Olivia Bauso on Unsplash")

## The Euphoria of Smartness

You start out writing some code for a task. You hit a few roadblocks. You surmount them. You write some more code. It works! Yes, you’re a beast. You’re the shredder, shredding your way through every engineering problem. Nothing can stand before you. Nothing can outwit the shredder. They always bend the knee.

You look at your code again. It looks so clever. You pat yourself on the back. No one understands how your hand manages to reach your back but it does. Then again, you’re the shredder. You can do anything.

You tell your friends about your smart solution. They can’t believe the smartness! They’re like:

>  All Hail The Chosen One

They say to themselves, *“Oh, that we may touch the hem of his garment . . .”.*

## The Plateau

You have crafted a solution that required you to dig into the deepest recesses of cleverness — depths of smartness you never realised you possess. You have even gone ahead to solve problems you presume you might have in the future. Wow, you are so foresighted!

Again you lift your hand, move it to your back and pat yourself a few times more. You’ve done a smart job. Now, you feel exhausted from expending all that smartness. You get some rest. You can’t dwell on your laurels, so you move on to the next task.

You trot on, writing more code that make use of your clever code. You extend it to handle more use cases and edge cases. Your codebase revolves around your smartness.

## The Spiral

One week later, you’ve all but forgotten about your clever solution. You’ve dredged up several other intelligent and not so smart solutions to other problems. Suddenly, there’s a problem in the part of the project you worked on from a week ago. You’re the smart dude who coded the god-level solution, so you’re asked to fix it. You step down from your throne. You’re just gonna spend a second on this problem. It’s only a challenge for mere mortals. Not you.

One second turns into a minute. A minute into a day. You can’t understand why the problem exists or how to solve it. You can’t understand the flow of data or logic. You remember you reached for some extra depths of cleverness so you channel some inner *chi* hoping to reach for extra smartness again.

![Photo by \[Indian Yogi (Yogi Madhav)\](https://unsplash.com/@yogimadhav?utm_source=medium&utm_medium=referral) on \[Unsplash\](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/10368/0*2t4Wonnm0U9BWUVi)*Photo by [Indian Yogi (Yogi Madhav)](https://unsplash.com/@yogimadhav?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

Days roll into each other. You raise your head and a week has gone by. You’ve churned out many smart solutions but they’ve all been inadequate. Each solution unveils another problem. Each solution destroys your application. Alas, you’ve met your match — a load-bearing bug. You have been defeated. You cry out for help.

![Photo by \[Holger Link\](https://unsplash.com/@photoholgic?utm_source=medium&utm_medium=referral) on \[Unsplash\](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/6450/0*HKxfTjTVKwDKO6uE)*Photo by [Holger Link](https://unsplash.com/@photoholgic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

This is a self-fulfilling prophecy. Every developer I’ve met has been through one or more episodes of the tale above. If you haven’t, your experience is probably around the corner.

## The Paradox of Smart Solutions

> Everyone knows that debugging is twice as hard as writing a program in the first place. So if you’re as clever as you can be when you write it, how will you ever debug it? – Brian Kernighan. “[The Elements of Programming Style](https://en.wikipedia.org/wiki/The_Elements_of_Programming_Style)”, 2nd edition, chapter 2.

Coming up with clever solutions and premature optimisations almost always leads you down this road — a world of pain. If you maintain the project long enough, you’ll run into this situation. You’ll end up having to dumb things down a bit, make things less dry, rewrite all the code that extends or depends on your **highly** optimised clever code. Save yourself some headache, do not optimise working code unless it’s clearly a bottleneck. When you do, over-communicate the optimisation with explicit comments and documentation. Your optimisations should be for readability and maintainability.

Don’t optimise for problems that may occur in future. In my experience, those problems usually never occur, and when they do occur, the preemptive solutions are often inefficient. In retrospect, you end up spending so much time for so little return, if any.

This is a familiar terrain for experienced developers. Over the years, they’ve learned to stay dumb. They write dumb code and begrudgingly introduce smartness only when necessary. They solve the problem at hand, howbeit holistically. They don’t solve imaginary problems they make up or think they might someday have. They solve the problems they have.

Be Dumb. Your future self would thank you.