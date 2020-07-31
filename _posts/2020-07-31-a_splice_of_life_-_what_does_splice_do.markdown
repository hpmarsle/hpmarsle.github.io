---
layout: post
title:      "A Splice of Life - What does .splice() do?"
date:       2020-07-31 19:46:38 +0000
permalink:  a_splice_of_life_-_what_does_splice_do
---


### This ~~split~~ is bananas. B-A-N-A-N-A-S. This splice is bananas. B-A-N-A-N-A-S
This article will cover a use case of the Javascript mehtod *.splice()* and a mnemonic device of a banana split to remember it's arguments.  
***Note: Do not confuse our mnemonic banana split for the Javascript string method .split(). We are covering the array method .splice() in this article.***

![delicious banana split shown with chocolate sauce, whipped cream, and candied cherries](https://assets.wsimgs.com/wsimgs/ab/images/dp/recipe/201943/0024/img90l.jpg)

## .splice() 
  
Let's first go over the definition of the .splice() method from the [MDN web docs](https://help.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository ) and look at an example.  

> The splice() method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.

```
const friends = ['Harry', 'Ron', 'Hermione', 'Neville', 'Cedric'];
friends.splice(3, 0, 'Luna');
// inserts 'Luna' at index 3
console.log(friends);
// expected output: Array ['Harry', 'Ron', 'Hermione', 'Luna', 'Neville', 'Cedric']

const days = ["Monday", "Tuesday", " Wine", "Thursday", "Friday", "Saturday", "Sunday"]
days.splice(2, 1, "Wednesday")
// replaces 1 element at index 2 "Wine" with "Wednesday"
console.log(days);
// expected output: Array ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
```

## To the Ice Cream Parlor!

Now that we have a genral idea of how .splice() works, we'll dive further into some use cases and how to remember what each parameter does using our banana split analogy. 

We are at the ice cream parlor, and we see a big chalkboard on the wall. In big capital letters it says MENU: BANANA SPLIT, 3 scoops of vanilla ice cream, bananas, chocolate syrup, whipped cream, and cherries.' I personally like caramel syrup over chocolate and love strawberries with my ice cream, so I ask the attendant if I can take out the chocolate syrup, and add my 2 preferred ingredients. He smiles and points to an additional pamphlet that has a full list of optional toppings with both strawberries and caramel sauce on it! Then he says to us:

>##  We have only one menu item, the banana split, but you can splice it how you like it!


<img src="https://images.squarespace-cdn.com/content/v1/53264480e4b0c0f6fcfe3e89/1593128645047-LTUMUEIBRFE927C2SL0X/ke17ZwdGBToddI8pDm48kDZOCC1hxjAuvg_TbOcQw1J7gQa3H78H3Y0txjaiv_0fDoOvxcdMmMKkDsyUqMSsMWxHk725yiiHCCLfrh8O1z5QPOohDIaIeljMHgDF5CVlOqpeNLcJ80NK65_fV7S1UUELhO1mqWcIVlsEijhhkWvTh8dpx8MnIzIounKXgvEqm7cT0R_dexc_UL_zbpz6JQ/Digital-TV-Menu_150--_Sundae2.gif" width="600">


Let's think of our original array as the banana split on the menu that comes as is:  
```const bananaSplit = ["vanilla ice cream", "bananas", "chocolate syrup", "whipped cream", "cherries"]```

```.splice()``` takes in 3 parameters, with only the first being a required argument:
1. start (the index position where you want to start altering your array)
2. deleteCount** (the number of items you want to delete starting at the given index)
3. additionalItems** any additional items you want to add at the index given for the first argument.
> **optional arguments

So in our banana split analogy, our method would look like this for my order:  
``` const unwantedToppings  = bananaSplit.splice(2, 1, "caramel sauce", "strawberries")```

**.splice()** is mutating the original array, but its return value is going to be an array of the items we are deleting from the original array. 

```
console.log(bananaSplit)  
// expected output: Array ["vanilla ice cream", "bananas", "caramel sauce", "strawberries" "whipped cream", "cherries"]

console.log(unwantedToppings) 
// expected output: Array ["chocolate syrup"]
```
**Steps in remembering how to use splice from the banana split analogy:** 
- The original array is our starting banana split.
- The first argument is where in the list of ingredients (index), do we want to start changing the banana split.
- The second optional argument: How many toppings are we deleting from that index?
- Additional arguments: Do we want to add any different toppings to our sundae at that index?

I hope this analogy helps you remember how to use splice!  

![](https://thumbs.gfycat.com/SpicySnoopyKite-size_restricted.gif)

Happy coding!  
Mars
