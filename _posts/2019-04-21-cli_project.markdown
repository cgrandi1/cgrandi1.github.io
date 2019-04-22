---
layout: post
title:      "CLI Project"
date:       2019-04-22 00:28:49 +0000
permalink:  cli_project
---



The CLI project was a difficult project, but a project I'm so grateful for. It felt like a culmination of everything I've learned so far. 

My thought process was this was to take one step at a time and don't over think of everything (something I tend to do).  I wanted to show the list of 76ers players, then when selecting the player it shows you their bio. To begin, I first started with the  Scraper Class

The scraper class was simply scraping information from the 76ers website. For each player, I scrapped the name, number, weight, height, date of birth, country their from, where they played prior the NBA, and number of years being a pro. Then i wanted to create that data into objects and give it attributes. That's where I did `new_player = Player.new(name)`. 

I created a player class to create objects. I also created a class variable `@@all = []` to push the ojects into an array. Then to call that array, I created a class method: `self.all`. Then I needed to create my ClI class to put my project into motion. 

In the CLI class I created a skeleton of what I wanted my project to do: 
`  welcome
   show_players
    select_player
    show_player_bio
    goodbye`.
		
My welcome class was simply an instance method introducing my project.

My `show_players` method would show a list of players. I would do that by showing the index and the name of each player. 

My `select_player` method is my interactive method where there is an input. In this method you select the number of a plyer then it returned their bio. I have conditionals in my method so if you want to exit, you simply enter in exit. After you select a number of the player, you then have the option of selecting a new player or exiting the project. If you enter in an invalid output, you will simply get a message saying "Invalid", then show you the list of players again. 

Show_player_bio simply shows the bio of the player. 

And goodbye method says "Thanks for using my CLI"


