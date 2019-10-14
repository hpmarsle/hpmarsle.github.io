---
layout: post
title:      "Your CLI gem for Glass Skin"
date:       2019-10-14 00:59:17 -0400
permalink:  your_cli_gem_for_glass_skin
---

### Introduction

Hello fellow coders!

This is my first CLI gem application. I wanted to make a program that combines my love of learning code with another passion of mine, skincare! Growing up, I've struggled with eczema ever since infancy. It comes and goes, but more than doctors, Korean skincare and a holistic approach to help does my skin best.

My app scrapes data from [peachandlily.com](http://). The founder of the company struggled with similar skin issues to mine, and I want to introduce others to the products that have helped my skin health improve so much, so maybe they can help them too! I wanted to make an app for those new to Korean skincare and could easily acess suggestions from their command line. 

As of right now, the gem only gives a user the summary of the skin concern they select. Another update needs to be made to scrape all the products from the website and display them to the user.

### Getting Started

For now, I have a working application!
To run the program install the gem to your command line by typing the below:
```
$ gem install skincare_cli_gem
```
After installation run:

`$ ./bin/skincare_cli_gem to run the application`

This will start the program with a welcome message and menu, and ask the guest to pick a skin concern they would like to learn more about. Their choices are acne, anti-aging, dryness, and sensitive skin. After entering a prompt, they will receive a summary of their skincare concern.
```
Welcome to your skincare collections.
----------------------------------------

Skin Concern Menu
1. Acne
2. Anti-aging
3. Dryness
4. Sensitive Skin

Please type the corresponding number to your skin concern, type list for the options, or type exit to leave:
```
Say they input 1. The user will see the below:
```
Acne
Anyone who suffers from persistent blemishes knows you can’t get rid of them fast enough. But if the acne products you’ve tried have had spotty results, put our top-rated Korean treatments to the test. (After all, Asian women prize creamy-smooth skin, so you know their anti-acne arsenal means business.) These solutions for acne-prone complexions will clear the way for more beautiful skin in no time.
```

### Sraping
This data is coming directly from the peachandlily.com webpages. I built a scraper class to firstly access the Peach and Lily website and create the initial menu by pulling the text from the filter options directly on the main page's menu bar. 

Then to provide the summary for each skin concern, I accessed my SkinConcern class's class method .all and used the .each method to scrape the individual web pages based on the ending path of the skin concern's name(acne, anti-aging, dryness, or sensitive skin).

My scraper.rb file is below:

```
class Scraper
    attr_accessor :concern, :doc

    def initialize 
        @doc = Nokogiri::HTML(open("https://www.peachandlily.com/collections/skin-concern"))
    end 

    def scrape
        scrape_menu
        scrape_concern_pages
    end

    def scrape_menu
        @concerns = @doc.search("#filter-items > div:nth-child(2) > ul > li label").collect{|concern|concern.text.strip}
        @menu = @concerns.values_at(0,1,3,11)
   
        @menu.each{|name|SkinConcern.new(name)}
    end 

    def scrape_concern_pages
        
        SkinConcern.all.each do |concern|
            web_page = Nokogiri::HTML(open("https://www.peachandlily.com/collections/#{concern.name.downcase.gsub(" ", "-")}"))
            if concern.name == "Dryness"
                concern.summary = web_page.search("#collection-description > span").text.strip
            else 
                concern.summary = web_page.search("#collection-description").text.strip
            end 
        end
        
    end
end
```

#### An error I encountered was scraping the summary for the Dryness concern

When I first started scraping each of the concern's web pages, I found they each had the same css selector I needed to iterate through my SkinConcern objects. However, when I tested the application, I ran into something ugly when I selected 3 from my menu for the Dryness skin concern:

```
<!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
-->
Overly dry, chapped, flaky skin doesn’t look good on anyone—and it feels even worse. What’s even more frustrating is that there’s a laundry list of causes that can occur at any time of year: winter weather and indoor heat, too much sun or chlorine, everyday aging, skin conditions like eczema, or harsh products (from your pre-Peach and Lily days, of course). Products for dry skin need to replenish thirsty complexions with intense moisture, and that’s exactly what these super-quenching formulas deliver.
```

I settled on a solution to add an if statement as my conditional just for that one concern.

```
def scrape_concern_pages
        
        SkinConcern.all.each do |concern|
            web_page = Nokogiri::HTML(open("https://www.peachandlily.com/collections/#{concern.name.downcase.gsub(" ", "-")}"))
            if concern.name == "Dryness"
                concern.summary = web_page.search("#collection-description > span").text.strip
            else 
                concern.summary = web_page.search("#collection-description").text.strip
            end 
        end
        
    end
```

```
Dryness
Overly dry, chapped, flaky skin doesn’t look good on anyone—and it feels even worse. What’s even more frustrating is that there’s a laundry list of causes that can occur at any time of year: winter weather and indoor heat, too much sun or chlorine, everyday aging, skin conditions like eczema, or harsh products (from your pre-Peach and Lily days, of course). Products for dry skin need to replenish thirsty complexions with intense moisture, and that’s exactly what these super-quenching formulas deliver.
```

### The Interface
See my video demo to see what the final product looks like!

[https://youtu.be/q3qaR-ZeP3o](http://)

### Moving Forward
Since I was pressed for time, I found this to be my best option, and I'll go back and refactor. I really want to add more features. I need to go another level deep and make a Product class that has a relationship with the SkinConcern class and also has a name, brand, and price. If I have even more time to brush up on it, maybe I can figure out how to pull product reviews! This project was very intense! I felt really stuck just getting started. Once I got setup on github thanks to a fellow classmate, I felt working on this was really fun. 

Overall, I had so much . I know the struggle is a part of the journey, and I'll always have more to learn. I can't wait to improve on this project and keep learning how to be better at programming. I hope you enjoyed this overview.

Thank you fo reading. Wishing you great skin health and happy coding! 
