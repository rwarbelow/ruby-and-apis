---
title: Storing and Manipulating Data with Hashes
layout: post
date: 2015-11-21 23:59:56
permalink: storing-and-manipulating-data-with-hashes
---

In this section, we'll store and access data in hashes. Hashes are best described as dictionaries or key-value pairs. You might want to take a look at the [Hash docs](http://ruby-doc.org/core-2.2.3/Hash.html). 

Hashes can look either of these ways (examples from Ruby Docs):

{% highlight ruby %}
options = { :font_size => 10, :font_family => "Arial" }
options = { font_size: 10, font_family: "Arial" }
{% endhighlight %}

<h4>Removing Elements from a Hash</h4>

{% highlight ruby %}
options = { :font_size => 10, :font_family => "Arial" }

options.delete(:font_size)
# this removes the key and value :font_size => 10 and returns the value
{% endhighlight %}

<h4>Adding Elements to a Hash</h4>

{% highlight ruby %}
options = { :font_size => 10, :font_family => "Arial" }

options[:font_weight] = "bold"
# this adds an additional key-value pair
{% endhighlight %}

<h4>Accessing Values Using Keys</h4>

{% highlight ruby %}
options = { :font_size => 10, :font_family => "Arial" }

options[:font_family]
# this will return the value associated with the :font_family key
{% endhighlight %}

<h4>Replacing Elements in a Hash</h4>

{% highlight ruby %}
options = { :font_size => 10, :font_family => "Arial" }

options[:font_family] = "Helvetica"
# this will overwrite the value "Arial" to be "Helvetica"
{% endhighlight %}

<h4>Counting Elements in a Hash</h4> 

{% highlight ruby %}
clothing = ["socks", "shirts", "gloves", "dresses", "pants"]

clothing.count
clothing.size
clothing.length
# these methods will return the number of key-value pairs
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Gift List, v.2.1</span>
    <p>Open your file `gift_list.rb`</p> <br>
    <p>
      Modify your program to save each user input in a `gifts` hash. The key will be the string value of the gift and the value will be the number of times that gift has been entered. For example: { "iPhone" => 1, "chocolate" => 3 }. Note: The keys will need to be stored as strings, not symbols like the above examples. 
    </p>
    <br>
    <p>
      After the gift is submitted, print out the number of times that specific gift has been entered. 
    </p>
    <br>
    <p>
      Hint: You may want to look into setting a default value for a hash (see <a href="http://ruby-doc.org/core-2.0.0/Hash.html#method-c-new">here</a>) and increasing that value using `+= 1`. 
    </p>
  </div>
</div>