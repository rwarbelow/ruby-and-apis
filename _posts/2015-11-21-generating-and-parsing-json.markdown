---
title: Generating and Parsing JSON
layout: post
date: 2015-11-21 23:59:48
permalink: generating-and-parsing-json
---

In this section, we'll use the [JSON module](http://ruby-doc.org/stdlib-2.2.4/libdoc/json/rdoc/JSON.html) of the Ruby standard library in order to generate JSON from Ruby objects and parse JSON strings into Ruby objects. 

`require 'active_support/all'`

{% highlight ruby %}
JSON.parse(card, :symbolize_names => true)
{% endhighlight %}

<h1>skdhf</h1>


{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

<h4>fldksh</h4>


{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}


`https://www.coursehero.com/api/flashcards/sets/600582/?api_key=INSERT-KEY-HERE`

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