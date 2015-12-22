---
title: Flashcard Game
layout: post
date: 2015-11-21 23:59:47
permalink: flashcard-game
---

Create a game whose interface works like this:

{% highlight ruby %}
require_relative 'card_generator'
require_relative 'round'

print "Welcome! Enter the name of the CSV file for your deck: "

file = gets.chomp
# This file should look something like "example-cards.csv".

cards = CardGenerator.new(file).create_cards
# This method should return an array of shuffled card objects

round = Round.new(cards)
round.start
# This should begin the game. The game will iterate through all cards 
# in the round and ask the user for an answer. The answers should be
# stored by the round.

# At the end of the game, the round should tell the user how many
# questions were answered correctly. Then, the program should
# save the results to a CSV where the headers are 
# question, answer, user_response, result (correct or incorrect)

puts "Your results have been saved to 'results.csv'."
puts "Thank you for playing!"
{% endhighlight %}

Here is some CSV data you can use for the card file:

```
question,answer
question1,answer1
question2,answer2
question3,answer3
question4,answer4
```

An example of the results.csv file might look like this:

```
question,answer,user_response,result
question2,answer2,answer2,true
question4,answer4,answer4,true
question3,answer3,question3,false
question1,answer1,answer1,true
```

Let's brainstorm some of the objects, behaviors, and attributes that we might want in this program. 

#### Extensions

1. Check whether or not the CSV file exists. If it does not, prompt the user to enter a new filename.
1. Instead of prompting the user for a filename, accept a filename as a command line argument (ie `$ ruby flashcards.rb card-data.csv`)
1. Output your results into JSON format. 
1. Allow both CSVs and text files containing JSON to be used for card data.
1. Use [Time.now](http://ruby-doc.org/core-2.2.3/Time.html#method-c-now) to generate a dynamic results file name.
1. Put incorrectly answered cards back into the iteration to be asked again.
1. Build in hint functionality. If a user enters "hint" when it's time to answer, the game should display a hint. In order to make this functional, you'll need to modify the CSV file you take in. 