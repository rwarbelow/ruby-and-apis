---
title: Scripting Find and Replace
layout: post
date: 2015-11-21 23:59:52
permalink: scripting-find-and-replace
---

In this section, we'll learn about the string method `#gsub` and figure out how to take in command-line arguments to use in a Ruby program. We'll use these tools to create a command-line program that can read in a file, find and replace content, and write the output back into that file.  

#### String method `#gsub`

[#gsub](http://ruby-doc.org/core-2.2.4/String.html#method-i-gsub) is a method for global substitution. It accepts two arguments: one for the pattern or word to find, and one for the replacement:

{% highlight ruby %}
text = "Here is a piece of text."
new_text = text.gsub("text", "candy")
{% endhighlight %}

This example will create a new string and leave `text` intact. If you want to permanently modify the existing string, use `gsub!` instead:

{% highlight ruby %}
text = "Here is a piece of text."
text.gsub!("text", "candy")
{% endhighlight %}

<h4>Command line arguments with `ARGV`</h4>

The variable `ARGV` represents any arguments from the command line. If I were to type:

{% highlight css %}
$ ruby my_program.rb panda batman
{% endhighlight %}

Then I could access "panda" and "batman" in `my_program.rb` like this:

{% highlight ruby %}
first_word  = ARGV[0]
second_word = ARGV[1]

# OR

first_word, second_word = ARGV
{% endhighlight %}


<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Scripting Find and Replace</span>
    <p>
      Build a Ruby program that is executed with the following command:
      {% highlight css %}
      $ ruby find-and-replace.rb cheese-ipsum.txt brie cheddar
      {% endhighlight %}
      <li>`find-and-replace.rb` is the filename of your program</li> 
      <li>`cheese-ipsum.txt` is the file containing the existing text</li> 
      <li>"brie" is the word that you're looking for, and "cheddar" is the word you want to put in place of "brie".</li>
    </p><br>
    <p>Print the revised draft to the screen and ask the user if they want to write over the existing file. If so, save the new text to the `cheese-ipsum.txt` file.</p> <br>
    <p>
      Here's some text you can use for the `cheese-ipsum.txt` file:

      {% highlight css %}
Croque monsieur feta swiss. Blue castello mozzarella cheese strings the big cheese emmental cheeseburger airedale chalk and cheese. Mozzarella the big cheese the big cheese port-salut croque monsieur brie camembert de normandie swiss. Roquefort taleggio fromage cheesy grin caerphilly mozzarella the big cheese when the cheese comes out everybody is happy. Macaroni cheese edam goat fromage frais cut the cheese caerphilly hard cheese cheese strings. Croque monsieur pecorino mascarpone airedale cheeseburger pepper jack gouda pepper jack. Fromage fondue st. agur blue cheese boursin swiss cow boursin airedale. Cheeseburger port-salut cream cheese squirty cheese cheesy feet cheese strings.

Parmesan macaroni cheese cut the cheese. Camembert de normandie cheese triangles bavarian bergkase boursin everyone loves blue castello swiss taleggio. Chalk and cheese fromage pecorino cheese strings brie hard cheese hard cheese brie. Squirty cheese cow edam queso caerphilly cauliflower cheese chalk and cheese say cheese. Halloumi or manchego cheesy grin squirty cheese halloumi taleggio melted cheese bavarian bergkase. Queso roquefort edam dolcelatte mozzarella pepper jack cheese and biscuits say cheese. Cheese and biscuits roquefort roquefort when the cheese comes out everybody is happy brie cheddar when the cheese comes out everybody is happy who moved my cheese. Babybel.

Danish fontina mascarpone who moved my cheese. Fromage who moved my cheese cheesy feet say cheese bocconcini rubber cheese stilton boursin. Monterey jack everyone loves stinking bishop when the cheese comes out everybody is happy cow cheese triangles cut the cheese cottage cheese. Melted cheese airedale cottage cheese halloumi danish fontina or monterey jack macaroni cheese feta. Parmesan danish fontina smelly cheese cheesy feet bocconcini squirty cheese goat lancashire. Brie taleggio say cheese st. agur blue cheese cheese and wine cauliflower cheese taleggio who moved my cheese. Cheese and wine feta bocconcini cheese slices bocconcini stinking bishop cheese and biscuits fondue. Cheese on toast manchego paneer melted cheese say cheese stilton squirty cheese cheese and biscuits. Mozzarella.

Cheeseburger edam croque monsieur. Stinking bishop say cheese cream cheese halloumi brie when the cheese comes out everybody is happy mozzarella mozzarella. Cut the cheese red leicester blue castello bocconcini boursin halloumi when the cheese comes out everybody is happy cheese and biscuits. Chalk and cheese who moved my cheese lancashire taleggio cheese on toast everyone loves monterey jack macaroni cheese. Dolcelatte stinking bishop halloumi feta brie danish fontina fromage frais everyone loves. Mozzarella who moved my cheese dolcelatte monterey jack.
      {% endhighlight %}
    </p>
  </div>
  <div class="card-content card-action orange-text">
    <span class="activator orange-text">answer</span>
  </div>
  <div class="card-reveal">
    <span class="card-title orange-text">close</span>
    <p>Here is one possible solution:</p>
{% highlight ruby %}
file, find, replace = ARGV

text = File.read(file)
new_contents = text.gsub(/\s#{find}\s/, " #{replace} ")

puts "Here is the draft:"
puts "----------------"
puts new_contents
puts "----------------"

puts "Do you want to override the existing contents?"
answer = $stdin.gets.chomp
if answer == "yes"
  File.open(file, "w") {|f| f.write new_contents }
  puts "File has been updated."
end
{% endhighlight %}
  </div>
</div>

Curious about why you need to use `$stdin.gets.chomp` instead of `gets.chomp`? Check out this [StackOverflow answer](http://stackoverflow.com/questions/10523536/whats-the-difference-between-gets-chomp-vs-stdin-gets-chomp).

If you're interested in using Regex patterns, check out [rubular](http://rubular.com/) which is a playground for Ruby Regular Expressions. 