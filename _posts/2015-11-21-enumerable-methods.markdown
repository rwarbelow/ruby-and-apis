---
title: Enumerable Methods
layout: post
date: 2015-11-21 23:59:55
permalink: enumerable-methods
---

The [Enumerable module](http://ruby-doc.org/core-2.2.3/Enumerable.html) provides methods for collection classes like Array and Hash. The enumerable methods are built on top of the `#each` method. 

#### Anatomy of an enumerable method

collection.enumerable_method do |block_parameter|
  # code to be executed for each element
end

#### `#each`

{% highlight ruby %}
words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "pencil"]

words.each do |word|
  puts "Iterating over #{word}."
end
{% endhighlight %}

{% highlight ruby %}
words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "pencil"]

words.each do |word|
  if word[0] == "p"
    puts "#{word} begins with 'p'."
  else
    puts "#{word} does not begin with 'p'."
  end
end
{% endhighlight %}

<h4> `#each_with_index`</h4>

{% highlight ruby %}
words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "pencil"]

words.each_with_index do |word, index|
  puts "#{word} is at position #{index}."
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Iterating with #each_with_index</span>
    <p>
      Modify your gift list program so that all of the gifts are printed out with their index position number next to them.
    </p>
  </div>
</div>

#### `#map`

`#map` returns a new array that contain the values in the block. 

{% highlight ruby %}
plain_words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "pencil"]

terrific_words = plain_words.map do |word|
  "#{word}riffic!"
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Returing a new array with #map</span>
    <p>
      Write a piece of code that iterates over names and returns a new array where every name is upcased. 
    </p>
  </div>
</div>

Note: This method is also aliased as `#collect`. 

#### `#sort_by`

This method returns a new array where the elements are sorted by whatever the block specifies. 

{% highlight ruby %}
words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "pencil"]

sorted_words = words.sort_by do |word|
  word.length
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Returing a sorted array with #sort_by</span>
    <p>
      Write a piece of code that iterates over names and returns a new array where the names are sorted alphabetically.
    </p>
    <br>
    <p>
      BONUS: In an array of first and last names, return the names sorted alphabetically by last name. You'll want to use the `#split()` method in order to separate first and last names.<br>
      names = ["Bob Jones", "Ann Smith", "Carol Johnson", "Maria Miller"]
    </p>
  </div>
</div>

#### `#reduce` 

`#reduce` is a strange method because it can do a variety of things. We're going to use it for one thing today:

{% highlight ruby %}
numbers = [10, 20, 15, 8]

result = numbers.reduce do |sum, num|
  sum + num
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Multiplying several numbers</span>
    <p>
      Write a piece of code that iterates over an array of numbers and returns the product of all numbers in the array. 
    </p>
  </div>
</div>

Note: This method is also aliased as `#inject`.

#### `#select`

`#select` returns a new array that only contains elements for which the block evalutes to true (or truthy).

{% highlight ruby %}
numbers = [9, 3, 4, 8, 12, 15, 19]

evens = numbers.select do |num|
  num.even? 
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Selecting the 'ings'</span>
    <p>
      Write a piece of code that iterates over an array of words and returns a new array that only contains words ending in "ing".  
    </p>
  </div>
</div>

Note: This method is also aliased as `#find_all`.

#### `#find`

`#find` is similar to select in that it looks for truthiness in the block, but it only returns the <b>first</b> element it finds for which the block evalutates to true. If no elements are found, the return value is `nil`.

{% highlight ruby %}
numbers = [9, 3, 4, 8, 12, 15, 19]

first_even = numbers.find do |num|
  num.even? 
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Finding an element</span>
    <p>
      Write a piece of code that iterates over an array of numbers and finds the first number that is larger than 100.  
    </p>
  </div>
</div>

Note: This method is also aliased as `#detect`.

#### `#reject`

`#reject` returns an array where elements for which the block returns true are removed. 

{% highlight ruby %}
numbers = [9, 3, 4, 8, 12, 15, 19]

odds = numbers.reject do |num|
  num.even? 
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Rejecting empty strings and nil</span>
    <p>
      Write a piece of code that iterates over the array below and returns a new array where there are no empty strings or nil values. 
    </p> <br>
    <p>
      packing_list = ["toothbrush", nil, "shampoo", "cell phone", "", "", "credit card", nil]
    </p>
  </div>
</div>

#### `#all?`, `#any?`, and `#none?`

These three methods return either `true` or `false` depending on whether or not all, any, or none of the elements meet a certain condition. They do not return a new array. 

{% highlight ruby %}
numbers = [9, 3, 4, 8, 12, 15, 19]

odds = numbers.any? do |num|
  num.even? 
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Filtering with a predicate enumerable method</span>
    <p>
      Write a piece of code that iterates over the array below and returns `true` if there are any elements that are of the class Integer and `false` if not. Hint: use the `is_a?(ClassName)` method for the block.
    </p> <br>
    <p>
      elements = ["hello", nil, "5", "1000", [2,1,6], { key: "value"}, ""]
    </p>
  </div>
</div>

#### `#group_by`

`#group_by` returns a hash where the key is the result of the block and the value is an array of the elements corresponding to that value. 

{% highlight ruby %}
words = ["pizza", "plant", "bicycle", "shoe", "dishwasher", "plastic"]

words.group_by do |word|
  word.length
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Grouping by first letter</span>
    <p>
      Write a piece of code that iterates over an array of words and groups them by the first letter.  
    </p>
  </div>
</div>

These are just some of the common enumerable methods. Check out the [Enumerable docs](http://ruby-doc.org/core-2.2.3/Enumerable.html) for more. 