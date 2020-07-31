---
layout: post
title:      "A Short Intro to React Hooks"
date:       2020-07-31 20:34:41 +0000
permalink:  a_short_intro_to_react_hooks
---

## We can use state in functional components!
![man gesturing something is incredible](https://www.reactiongifs.com/r/2013/03/mind-blown.gif)

With the implementation of hooks, React now allows us to use state without a class. We can use state in a functional component with the useState hook. 

## What is a Hook?

According to the React docs a hook is a special function that lets you “hook into” React features. 
Below I will give an example of a LikeButton component using the useState hook: 

## Example 

<img alt="code snippet example of functional component using the useState hook" src="https://i.imgur.com/9SlLVwi.png" width=600 />

In this example snippet, we are destructuring what the useState hook is returning.

You can think of our first destructured variable numOfLikes as "this.state" and our setCount function variable as "this.setState" like we would use in class components to reference state. The argument passed into useState(0) is setting our intial state of **numOfLikes: 0**.

When our LikeButton component is rendered, state will be updated everytime a user clicks the button! Very clean and cool! This is just a taste of what hooks can do.

You can read more about the cool features and implementation of what Hooks give us as React developers in the official
[React Hooks documentaiton](https://reactjs.org/docs/hooks-intro.html).



