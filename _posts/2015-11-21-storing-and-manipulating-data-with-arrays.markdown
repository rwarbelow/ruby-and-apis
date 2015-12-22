---
title: Storing and Manipulating Data with Arrays
layout: post
date: 2015-11-21 23:59:57
permalink: storing-and-manipulating-data-with-arrays
---

In this section, we'll store and access data in arrays. Think of arrays as boxes of data. You might want to take a look at the [Array docs](http://ruby-doc.org/core-2.2.0/Array.html). 

<h4>Removing Elements from an Array</h4>

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing.pop  
# this removes the last element of the array permanently and returns it

clothing.delete("gloves")  
# this removes the element that matches the argument
{% endhighlight %}

<h4>Adding Elements to an Array</h4>

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing << "hats"
clothing.push("hats")  
# these two methods are synonymous
{% endhighlight %}

<h4>Accessing Elements via Index Position</h4>

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing[0] # will return the first element "socks"
clothing[3] # will return the fourth element "dresses"
clothing[-1] # will return the last element "pants"
{% endhighlight %}

<h4>Replacing Elements in an Array</h4>

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing[0] = "boots"
# this will replace "socks" (element 0) with "boots"
{% endhighlight %}

<h4>Counting Elements in an Array</h4> 

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing.count
clothing.size
clothing.length
{% endhighlight %}

These three methods will return the same value. However, they have different implications for performance. You can read more about that [here](http://batsov.com/articles/2014/02/17/the-elements-of-style-in-ruby-number-13-length-vs-size-vs-count/). 

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Gift List, v.2.0</span>
    <p>Open your file `gift_list.rb`</p> <br>
    <p>
      Modify your program to save each user input in a `gifts` array. After each input from the user, print out how many total gifts have been entered. 
    </p>
    <br>
    <p>
      If the user enters the word "delete" instead of a gift, print out all of the gifts that have been entered so far. Then prompt the user to enter the position number they wish to delete. After they enter a number, delete that gift and continue prompting for a new gift.
    </p>
  </div>
</div>