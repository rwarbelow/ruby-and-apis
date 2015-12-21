---
title: Flashcard Game
layout: post
date: 2015-11-21 23:59:47
---

Create a game whose interface works like this:

{% highlight ruby %}
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

#### Extensions

1. Check whether or not the CSV file exists. If it does not, prompt the user to enter a new filename. 
1. Output your results into JSON format. 
1. Allow both CSVs and 