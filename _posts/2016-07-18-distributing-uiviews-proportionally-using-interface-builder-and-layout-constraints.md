---
layout:     post
title:      "Distributing UIViews proportionally using Interface Builder and Layout Constraints"
subtitle:   "Using Proportional Constraints"
date:       2016-07-18 19:27:00
author:     "Cedulio Cezar"
header-img: "img/post1/head.jpg"
tags: [ios,swift,proportional image view,dev,tips]
summary: "How to distribute UIViews proportionally using constraints"
comments: True
---
Create layouts in interface builder can be tricky sometimes, to me distributing views them proportionally was an example.

While this isn't so obvious at the first time, you will notice that is quite simple to achieve.

<img src="{{ site.baseurl }}/img/posts/proportional-constraints/proportional_views_final.png" alt="Final project">

#### TL;DR
What It's done here is basically add a container view that hold the UIViews that need be distributed proportionally and make all subviews to have the same width of it's parent with a multiplier which represents the percentage occupied in x axis.

As usual x and y layouts constraints are required to satisfy AutoLayout.

This blog post assumes that you have a basic knowledge about layout constraints.

## Let's do it in 10 steps!!

1. Create a new Simple View Project called ProportionalViews.

2. Open Main.storyboard and select the ViewController.

3. Create a container view that will hold both images.
Add a UIView (We will call it container) to the ViewController and pin it to the edges of it's parent.








## Don't Support Multiple screen

<img src="{{ site.baseurl }}/img/post1/android_support_multiple_screens.jpg" alt="Tweet complaining about support multiple screens">

Let's assume that now your app is handling the rotation correctly and you want to show to your friends what amazing app you created.

You sent the apk file to them, everything is fine, until some of them start to report that some screens of your app just don't show entirely or the components look strange filling the screen horizontally (oh boy).

This is a bit frustrating when you realize that you should have to create different '.xml' for every screen size.

You might be thinking that your app won't support large screens or the small ones, because it's difficult to do that. Again, don't that, because if you go this way you are wasting the most successful feature of Android platform, that it runs on a huge variety of devices.

One argument that you might think is that the app doesn't need to run on different devices. It can be true right now in your scenario, but even is these cases I recommend you learn how to create screens that support different sizes. I can tell you by experience that these kind of requirement can change really fast.

A place to start: [Android Screen Sizes](http://developer.android.com/training/multiscreen/screensizes.html)

## Neglecting UI & UX

At this moment your app it is running nicely through a variety of devices. You might end up asking some questions like:

- Why this isn't cool like apps from Google or Twitter?
- Should I be concerned about this even as a software developer?


The bad news is that the answer for the last question is, YES you have to think about these kind of things,  and good news is that Google already developed pattern called Material Design, that will help you to create amazing apps.

You can check that out here:
[Material Design Introduction](https://www.google.com/design/spec/material-design/introduction.html)



Before people that work as designers come here to complain about this I will explain myself. I know that this doesn't replace a UI & UX Engineer. But it's a good place start don't you think?


## Forget basic concepts of OOP

Now your app just rocketed, you have a great base of users and the features are popping out. Soon or later you will end up with a large code base and you will have to maintain and add more things.

You might be in trouble if you don't keep in mind that you are programming in a OOP language and should be decoupling and reusing code. It may look obvious talking like that, but believe me in Android Universe it is common to see developers mixing everything in one class like Fragment.java, creating many 'God Objets'.

hese God Objets do everything from presenting the data to the user, to access the database or network. This is a bad practice that difficult changes in code.

Instead of create God Objects, use patterns in code to design your app. One book that I recommend  that helps to keep your code easy to read and maintain is Clean Code of Robert C. Martin.

## Conclusion

While some of the problems are only related to Android development some are not, specially when talking about code maintenance.

What do you think?Would you add more points?

Please, let me know.

Image: Courtesy of Uncalno Tekno, avaiable at Flickr.<br/>Image License: Creative Commons 2.0.
