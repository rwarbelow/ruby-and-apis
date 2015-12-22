---
title: Reading from Files
layout: post
date: 2015-11-21 23:59:54
permalink: reading-from-files
---

In this section, we'll learn how to read in text files using the [File](http://ruby-doc.org/core-2.2.0/File.html) class in Ruby. Read more about the File class [here](https://rubymonk.com/learning/books/1-ruby-primer/chapters/42-introduction-to-i-o/lessons/90-using-the-file-class) on RubyMonk. 

`File.open(filename, 'r')` creates a Ruby handler to read with that file. Let's try it. First, create a text file `example.txt` with this content:

```
Here is the first line
And another line
Finally, one last line
```

Go into irb (`$ irb` from the command line) and try this out:

{% highlight ruby %}
f = File.open('example.txt', 'r') 
f.pos
f.read
f.pos
f.read
f.rewind
f.pos
f.readlines
f.pos
f.readlines
f.rewind
f.pos
f.close 
f.read
{% endhighlight %}

What do you notice happening in each of those methods? Why is it necessary to `rewind`? What does the return value of `f.pos` represent?

To see if a file exists, we can use `File.exist?(filename)`. Since this is a predicate method, it will return `true` or `false`. 

{% highlight ruby %}
File.exist?('example.txt') #returns true
File.exist?('nonexample.txt') #returns false
{% endhighlight %}

Other things you may want to do with files: 

{% highlight ruby %}
contents = ''

f = File.open('example.txt', 'r') 

f.each_line do |line|
  contents += line
end

f.close 

puts contents
{% endhighlight %}


{% highlight ruby %}
File.readlines('example.txt', 'r').each do |line|
  puts line
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Finding word counts in a file</span>
    <p>
      Write a program that reads in a file `coffee-ipsum.txt` and returns a hash with the word as the value and the number of times it appears as the key. For example: { "coffee" => 7, "sugar" => 2}.  
    </p> <br>
    <p>BONUS #1: Make your program case-insensitive. "Coffee" and "coffee" should be counted together, not separately.</p> <br>
    <p>BONUS #2: Get a word from the user, then print how many times that word appears in the text.</p>
  </div>
</div>

`coffee-ipsum.txt`:

Turkish strong chicory frappuccino lungo redeye fair trade galao barista grinder decaffeinated Strong turkish eu plunger pot rich qui organic wings body to go Trifecta flavour mug as saucer crema breve coffee aftertaste froth grounds that kopi-luwak saucer roast dark grinder flavour caramelization whipped Percolator seasonal ut robusta eu cinnamon acerbic Beans cafe au lait organic saucer organic crema affogato viennese pumpkin spice con panna dark galao pumpkin spice a instant Black cafe au lait decaffeinated doppio steamed cup id white mug cream eu dark brewed Grounds ristretto eu crema variety irish french press strong black chicory to go roast cortado fair trade Qui turkish sit kopi-luwak steamed mug seasonal organic shop redeye ristretto spoon redeye grounds blue mountain cafe au lait coffee Chicory decaffeinated french press instant iced decaffeinated french press cup robust ut grinder cream seasonal arabica half and half acerbic cultivar Eu cinnamon qui so qui caffeine java Sugar grounds aftertaste cinnamon barista arabica frappuccino lungo siphon coffee extraction acerbic siphon con panna irish trifecta coffee Coffee organic americano wings foam percolator beans shop turkish redeye milk organic that mocha whipped Iced lungo macchiato pumpkin spice mazagran doppio americano carajillo americano cinnamon variety so cup Cappuccino java body viennese arabica barista carajillo qui medium Rich redeye crema plunger pot cortado mazagran eu sit acerbic extra as crema siphon dark instant shop turkish Robust doppio coffee turkish sit beans foam turkish kopi-luwak et brewed at roast crema Con panna ut whipped siphon robusta sugar id rich ut macchiato mocha froth bar ristretto est white aftertaste kopi-luwak robust coffee aroma steamed chicory
