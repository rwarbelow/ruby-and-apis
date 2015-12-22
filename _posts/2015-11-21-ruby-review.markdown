---
title: Ruby Review 
layout: post
date: 2015-11-21 23:59:59
permalink: ruby-review
---

In this section, we'll review Ruby basics, including naming conventions, data types, objects and methods, iteration, conditionals, input/output, and variable scope.

#### Creating and executing Ruby files

```
$ touch review.rb
$ ruby review.rb
```
<div class="break"></div>

#### Variable Naming Conventions

Variable names should indicate what data the variable stores. Someone who did not write your program should easily be able to understand
what the program does based on variable and method names.

In Ruby, variable names should start with a lowercase letter and consist of lowercase letters and/or underscores. It is possible to use numbers, but it's not preferred. 

Including the name of the data type is frowned upon. 

<div>
YES:

{% highlight ruby %}
message      = "Hello, world"
animals      = ["fish", "red panda", "elephant"]
student_ages = { max: 12, ellie: 14 }
{% endhighlight %}

NO:

{% highlight ruby %}
myVar = "variable"
task_1 = "build cabinet"
foods_array = ["watermelon", "sandwich", "ice cream"]
{% endhighlight %}
</div>

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it:</b> Variable Names</span>
    <p>
      In your `ruby-review.rb` file, create three variables:
    </p> <br>
    <li>a string of text containing the search term for a find-and-replace method</li>
    <li>an array of final grades (as percentages) for English class</li>
    <li>a hash representing ingredients and amount called for in a recipe</li>
  </div>
  
</div>

<div class="break"></div>
#### Data Types

##### String

{% highlight ruby %}
"here is a string"
{% endhighlight %}

##### Integer

{% highlight ruby %}
48
{% endhighlight %}

##### Float

{% highlight ruby %}
3.14
{% endhighlight %}

##### Array

{% highlight ruby %}
[9,4,6,13,92]
{% endhighlight %}

##### Hash

{% highlight ruby %}
# "old syntax"
{ :key => "value", :another_key => "second value" }
# or
{ 
  :key => "value",
  :another_key => "second value" 
}

# "new syntax"
{ key: "value", another_key: "second value" }
# or
{ 
  key: "value",
  another_key: "second value" 
}
{% endhighlight %}

<h5>Symbol</h5>

{% highlight ruby %}
:category
:student_id
{% endhighlight %}

<h5>Boolean</h5>

{% highlight ruby %}
true
false
{% endhighlight %}

<h5>Regular Expression</h5>

Regular Expressions (also known as Regex) are used to match or scan for patterns in a string. We'll talk a little more about these later, but here's an example of a Regex that would match from the start of a string (`\A`) all lowercase letters `[a-z]` to the end of the string `\z`. 

{% highlight ruby %}
/\A[a-z]\z/
{% endhighlight %}

<div class="break"></div>
<h4>Objects and Methods</h4> 

Objects have methods that can be called upon them. For example:

{% highlight ruby %}
"my message".split(" ")
#=> ["my", "message"]
{% endhighlight %}

<h5>Common String Methods</h5>

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>String Methods and Ruby Docs</span>
    <p>
      Find and try out five methods from the <a href="http://ruby-doc.org/core-2.2.0/String.html">Ruby String Docs</a>. Add these methods to your `ruby-review.rb` file with comments to explain what they do.
    </p>
  </div>
</div>

<div class="break"></div>
#### Conditional Statements

If/elsif/else statements are examples of control flow. What goes after the `if` is something that will evalutate to `true` or `truthy`. 

{% highlight ruby %}
secret_number = 100

if secret_number > 0
  puts "The number is positive"
elsif secret_number < 0
  puts "The number is negative"
else
  puts "The number is 0"
end
{% endhighlight %}

Everything in Ruby is `truthy` except for `nil` and `false`. 

{% highlight ruby %}
message = ""

if message
  puts "There is a message"
else
  puts "There is not a message"
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Conditionals</span>
    <p>
      Create two conditionals:
    </p>
    <br>
    <li>Check if an array is empty. If it is, print that out to the screen.</li>
    <li>Check if a hash of groceries has the key :tomato. If it does, print out the value for that key. If it does not, print "No tomatoes".</li>
  </div>
</div>

<div class="break"></div>
#### Control Flow

While loops can also be used to determine what happens next in a program. Like the `if/else` statement, the expression after `while` should evaluate to `true` or `false`. 

For example:

{% highlight ruby %}
flowers = %w(daisy rose lily iris orchid)
# %w() is a shorthand for creating an array of strings

while flowers.any?
  current_flower = flowers.pop
  puts "Planting #{current_flower}."
end

puts "No more flowers."
{% endhighlight %}

<div class="break"></div>

<h4>Iteration</h4> 

We'll talk more about iteration in another section, but the most basic form of iteration is the `#each` method. This can be used on both hashes and arrays.

{% highlight ruby %}
flowers = %w(daisy rose lily iris orchid)

flowers.each do |flower|
  puts "Planting #{flower}."
end
{% endhighlight %}

It's important to remember that the return value of `#each` is <b>the original array</b>.

<p>Here's an example using `#each` on a hash:</p>

{% highlight ruby %}
groceries = { pickle: 5, apple: 3, zucchini: 8, jam: 2 }

groceries.each do |food, quantity|
  puts "You need #{quantity} #{food}s."
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Iterating Through a Hash</span>
    <p>
      Create a hash of universities and their tuition costs. Iterate over the hash and print out a string like this: "UC Denver costs $15,000 per year."
    </p>
  </div>
</div>

#### Input/Output

<li>`print` displays a value on the screen <b>without</b> a newline character at the end. The return value is `nil`.</li>
<li>`puts` displays a value on the screen <b>with</b> a newline character at the end. The return value is `nil`.</li>
<li>`gets` waits for input from the user and inserts a newline character at the end. The return value is the input from the user</li>
<li>`gets.chomp` waits for input from the user and slices off the newline character at the end. The return value is the input from the user</li>
<li>`gets.strip` waits for input from the user and slices off any whitespace at the beginning or end. The return value is the input from the user</li>

<b>It's important to remember that no matter what the user types (a number, brackets, etc.), the input always comes into the program as a string.</b>

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Gift List -- Getting User Input</span>
    <p>Start a new file `gift_list.rb`</p> <br>
    <p>
      Combine some of the skills we're reviewed. Write a simple program allows users enter gifts that they want. If the user enters a gift title that is longer than 20 characters, print "Don't be so greedy". The program should continue prompting the user for input until the keyword "done" is entered. The program should then print "Goodbye!"
    </p>
  </div>
</div>

#### Defining Methods

We'll focus mainly on defining methods on objects, but it's possible to define methods in the global namespace. After a method has been define, it needs to be called in order for the code to be executed:

{% highlight ruby %}
def multiply(first_num, second_num, third_num)
  first_num * second_num * third_num
end

puts multiply(3,4,5)
{% endhighlight %}

A method that returns either `true` or `false` is called a predicate method. The convention is to define these methods with a question mark at the end of the method name like this:

{% highlight ruby %}
def equal?(first, second)
  first == second
end

if equal?("message", "message")
  puts "The two arguments are equal."
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Defining Methods</span>
    <p>
      Define and call a method that squares a number.
    </p>
  </div>
</div>

#### Variable Scope

Not all variables are available everywhere within a program. For example, if a variable is defined within a method, it cannot be accessed outside that method. This will not work:

{% highlight ruby %}
def my_method
  numbers = [1,2,3,4,5]
end

puts numbers
# this will not work!
{% endhighlight %}