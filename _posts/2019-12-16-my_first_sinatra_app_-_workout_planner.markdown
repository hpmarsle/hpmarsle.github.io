---
layout: post
title:      "My First Sinatra App - Workout Planner"
date:       2019-12-16 05:47:34 +0000
permalink:  my_first_sinatra_app_-_workout_planner
---

Staring at a blank code editor seems to always make me freeze up at first. I had a harder time grasping the ActiveRecord and Sinatra labs so much that I fell behind, and before I knew it, it's time for the next project. I had no idea where to start, and I had so much to learn in order to complete just the minimum requirements for this project. Welp, in the words of Tim Gunn from Project Runway...

![](https://media.giphy.com/media/3o7TKGMZHi73yzCumQ/giphy.gif)

First, **make it work**. Then, make it pretty. 

To get started I thought about it first from the user's perspective. I drew out on regular paper what I wanted each page to have from sign up to logging in and their landing home page to list all of their exercises and links to add and edit those exercises. Then I created a to do list based on MVC and other notes for myself with what I needed to learn as I went through each step of my project. I went back and forth with the list of items I needed to learn and then back to the labs where I can learn those items, and then apply what I learned to my project!

**Models**
* User (has_many :exercises), need to learn user authentication and secure passwords
* Exercise (belongs_to :user)

**Views**
* root landing (app home page)
* log in (log in form needed) will validate matching username and pw
* sign up (signup form and create new user, log them in after success)
* index (home page when logged in)
* new (Create), form for new exercise, create new Exercise in db
* show(Read/Delete) show by id route, have hidden delete form and add Rack::MethodOverride to config.ru
* edit(Update) patch request, need form with values filled out, assign new user inputs to existing exercise
* warning (for if a user wants to edit an exercise that is not there's)


**Controllers**
* application controller need to learn sessions and helper methods I can use in other controllers
* user controller (will create, login, logout users)
* exercise controller (will handle ActiveRecord CRUD
cts

The final file  tree structure went like this. I used a great gem called tty-tree to populate this structure in my console.
Just run the following code for your future projects.
```
rake console
tree = TTY::Tree.new(Dir.pwd)
puts tree.render 
```

<a href="https://imgur.com/egVTd6v"><img src="https://i.imgur.com/egVTd6v.png" title="source: imgur.com" /></a>

## Next steps
Overall, of course my app is basic right now, and I want to add styling, but it's a working project!  I'm happy that I learned everything I needed to complete the basic requirements in the condensed time I had. My next steps are to add some CSS styling, so it will look like an app people will want to use! Another feature I want to add is for my clients to be able to categorize their exercises by weekdays as well!
