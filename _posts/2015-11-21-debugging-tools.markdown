---
title: Debugging Tools
layout: post
date: 2015-11-21 23:59:58
permalink: debugging-tools
---

In this section, we'll take a look at a few ways to debug Ruby code, including `puts` and a Ruby gem called `pry`.

#### `puts` or `p`

If you're not sure what a value is in your program at a certain point in tine, you can use `puts` or `p` to show that element. 

{% highlight ruby %}

2.2.2 :001 > percentage = 0.75 * 100
           => 75.0 
2.2.2 :002 > puts percentage
           75.0
           => nil 
2.2.2 :003 > p percentage
           75.0
           => 75.0 

{% endhighlight %}

{% highlight ruby %}
2.2.2 :001 > animals = ["cat", "dog", "raven"]
           => ["cat", "dog", "raven"] 
2.2.2 :002 > puts animals
           cat
           dog
           raven
           => nil 
2.2.2 :003 > p animals
           ["cat", "dog", "raven"]
           => ["cat", "dog", "raven"]
{% endhighlight %}

Let's try out using `puts` with this piece of code:

{% highlight ruby %}
flowers = %w(daisy rose lily iris orchid)
# %w() is a shorthand for creating an array of strings

while flowers.any?
  puts "Flowers before #pop: #{flowers}"
  current_flower = flowers.pop
  puts "Flowers after #pop: #{flowers}"
  puts "Planting #{current_flower}."
end

puts "No more flowers."
{% endhighlight %}

#### `pry`

Pry is a Ruby Gem (library of code) that can be used to stop execution at a certain point and look inside to see what is defined and what values exist. 

To try out pry, you'll need to install the gem: `$ gem install pry`

Then, let's take this piece of code from the Ruby Review and run it:

{% highlight ruby %}
flowers = %w(daisy rose lily iris orchid)
# %w() is a shorthand for creating an array of strings

while flowers.any?
  current_flower = flowers.pop
  require 'pry'; binding.pry
  puts "Planting #{current_flower}."
end

puts "No more flowers."
{% endhighlight %}

While in pry, `exit` will release your program from the pry and continue execution. `exit!` will exit the program completely without finishing. 

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Debugging with Pry</span>
    <p>
      Stick `require 'pry'; binding.pry` into your gift list program from the Ruby Review. What variables are available in which places? Can you see different values depending on which line you put the pry? 
    </p>
  </div>
</div>

#### Pseudocode

Pseudocode isn't exactly a debugging tool, but it can help you write a program without bugs. This is what pseudocode for a number guessing game might look like:

```
# set secret number
# get user guess
# check if user guess is the secret number
# if it is, print winning message
# if it is not, print "try again"
# continue to get input from user until guess is equal to secret number
```
