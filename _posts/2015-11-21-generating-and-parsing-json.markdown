---
title: Generating and Parsing JSON
layout: post
date: 2015-11-21 23:59:48
permalink: generating-and-parsing-json
---

JSON stands for JavaScript Object Notation. It is a machine- and human-readable format for data organization. 

In this section, we'll use the [JSON module](http://ruby-doc.org/stdlib-2.2.4/libdoc/json/rdoc/JSON.html) of the Ruby standard library in order to generate JSON from Ruby objects and parse JSON strings into Ruby objects. 

<h4>Generating JSON from Ruby Objects</h4>

To generate JSON, we'll need to require the JSON module:

{% highlight ruby %}
require 'json'
{% endhighlight %}

Anything can be turned into JSON. However, it's most powerfully used when Ruby hashes are passed:

{% highlight ruby %}
{ fruit: "apple", vegetable: "carrot" }.to_json
#=> "{\"fruit\":\"apple\",\"vegetable\":\"carrot\"}"
{% endhighlight %}

This might look funny. Those slashes are actually escape characters. They prevent the quotes from being closed prematurely. 

We can also turn nested hashes into JSON:

{% highlight ruby %}
{ foods: { fruit: "apple", vegetable: "carrot" }, furniture: { livingroom: "couch", bedroom: "dresser" } }.to_json
#=> "{\"foods\":{\"fruit\":\"apple\",\"vegetable\":\"carrot\"},\"clothing\":{\"outerwear\":\"coat\"}}" 
{% endhighlight %}

<h4>Parsing JSON into Ruby Objects</h4>

To parse JSON, we use `JSON.parse(data)`:

{% highlight ruby %}
data = "{\"fruit\":\"apple\",\"vegetable\":\"carrot\"}"
parsed_data = JSON.parse(data, :symbolize_names => true)
#=> {:fruit=>"apple", :vegetable=>"carrot"} 
{% endhighlight %}

Notice that `:symbolize_names => true` turned the keys into symbols (which is what we want). 

We can now access the data as we would any regular hash. 


<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Reading JSON from a File</span>
    <p>
      The data below is the result of an API call to `https://www.coursehero.com/api/flashcards/sets/600582/?api_key=INSERT-KEY-HERE`. 
    </p> <br>
    <p>You'll combine a few skills here. First, save the JSON below into a file called `flashcards.json`. Then, create a `Flashcard` ruby object. You'll notice that the only data values that are relevant are `term` and `definition`, so your Ruby object only needs to have those attributes. Read in the JSON data, then output an array of five `Flashcard` objects. </p>
  </div>
</div>

{% highlight json %}
{"flashcards": [
  {
    "fcid": 49410534,
    "order": 0,
    "term": "method",
    "definition": "A function that manipulates the output. These must begin with a lowercase. For example: first_name = gets.chomp.capitalize!",
    "hint": "",
    "example": "",
    "term_image": null,
    "hint_image": null
  },
  {
    "fcid": 49410535,
    "order": 0,
    "term": "gets",
    "definition": "accepts a single line of data from the standard input, and assigns the string typed to the variable",
    "hint": "",
    "example": "",
    "term_image": null,
    "hint_image": null
  },
  {
    "fcid": 49410536,
    "order": 0,
    "term": "chomp",
    "definition": "a string method and gets retrieves only strings from your keyboard. Gets returns a string and a newline character, while chomp removes this newline.",
    "hint": "",
    "example": "",
    "term_image": null,
    "hint_image": null
  },
  {
    "fcid": 49410537,
    "order": 0,
    "term": "capitalize!",
    "definition": "capitalizes the string, but does not make a copy becuase a \"!\" was used at the end.",
    "hint": "",
    "example": "",
    "term_image": null,
    "hint_image": null
  },
  {
    "fcid": 49410538,
    "order": 0,
    "term": "string",
    "definition": "An object in Ruby holds and manipulates an arbitrary sequence of one or more bytes, typically representing characters that represent human language. The simplest of these are enclosed in single quotes (the apostrophe character). The text within the quote marks is the value of this object.",
    "hint": "",
    "example": "",
    "term_image": null,
    "hint_image": null
  }
]}
{% endhighlight %}

<h4>Turing Custom Objects into JSON</h4>

Normally if you call `#to_json` on an object you've defined, you'll get something like this, which isn't helpful:

{% highlight ruby %}
require 'json'
person = Person.new({:first_name=>"Nancy", :last_name=>"Gonzalez", :email=>"ngonzalez0@mtv.com", :state=>"Florida"})
person.to_json
#=> "\"#<Person:0x007f95cc218d38>\"" 
{% endhighlight %}

However, we can require part of the `ActiveSupport` library (which is normally used in Rails), and get a much cleaner output for our JSON data:

{% highlight ruby %}
require 'json'
require 'active_support/all'
person = Person.new({:first_name=>"Nancy", :last_name=>"Gonzalez", :email=>"ngonzalez0@mtv.com", :state=>"Florida"})
person.to_json
#=> "{\"first_name\":\"Nancy\",\"last_name\":\"Gonzalez\",\"email\":\"ngonzalez0@mtv.com\",\"state\":\"Florida\"}" 
{% endhighlight %}
