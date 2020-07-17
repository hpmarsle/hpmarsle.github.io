---
layout: post
title:      "React and Routes "
date:       2020-07-13 14:36:31 -0400
permalink:  react_and_routes
---


## Route, Link, or NavLink?

With React Router it is easy to navigate a React App and render a Component based on the Route. Routes, Links, and NavLinks all sound very, so in this post, I am going to explain how to get started with React-Router and when to use each ot them for your React App.

First you'll run ```npm install --save react-router-dom``` in your project directory to include in your package.json file.

Then you can either initiate using the ```<BrowserRouter><BrowserRouter/>``` tags in your index.js or app.js file. I'll show you both ways that it can be done. In my app, I am also using redux, so this will also be reflected in the example code snippets.

###  Initiating in Index.js

Below I am importing BrowserRouter from 'react-router-dom'. The "as Router" refers to that we want to use an alias for ```<BrowserRouter>```, as ```<Router>```. You can see that this wraps around our main ```<App />``` component. BrowserRouter must have only one child component.

![index.js code snippet with react-router](https://i.imgur.com/mUynIiS.png)

Now you'll be able to use `<Route>` anywhere throughout your application if it's in your ```<App />``` component or a child component of it. I personally prefer the routes all under the App component, so I can view them together for reference.

###  Initiating in App.js


![index.js code snippet without react-router](https://i.imgur.com/Xnhu0lT.png)

When initiating in App.js, we will import it the exact same as the index.js example. We will wrap `<Router>` around the component's return value inside `<div className="App"></div>`.


![app.js code snippet with react-router](https://i.imgur.com/nth7zjR.png)

Then we can include our routes, by adding Route in our import statement, and then include Routes in our App div. the ```component={ComponentName}``` tells our Router which component we want to display at that route.

![app.js code snippet with react-router with routes](https://i.imgur.com/vGbQ9G5.png)

Now what is the difference between having Routes or links? Routes tell us which components to render. Links and NavLinks tell us to go to a Route. These are "clickable" and seen on the client-side. In my example app, I want to include a Navbar that will have links that will direct me to differenct route paths (i.e. /, /about, or /login)

![app.js navbar included](https://i.imgur.com/TgMTzm9.png)

In the Navbar component I'm exporting to App, we need to ```import { NavLink } from 'react-router-dom'```.

We can then use NavLinks in our Navbar. The title of the link will be between the opening and closing tags that the user will see. The ```to``` attribute's value will take us to the desired associated route when clicked.  ```to='pathAssociatedwithRoute'```

![navbar with navlinks](https://i.imgur.com/IOEesmi.png)


 But what about ```<Link>```. Is there any difference to ```<NavLink>```?

 The difference is you can add an "activeStyle" to your NavLinks to show which link is active for the route you are on! In our example, the active link in our navigation bar will have a solid white border bottom!

 I hope this tutorial was helpful and a good intro to React Router! 

 Happy coding!

 Mars
