---
title: OpenStruct to create Ruby objects on the fly
layout: post
date: 2015-01-04 23:59:56
permalink: openstruct
---

OpenStruct is part of the Ruby standard library. It is used to create objects on the fly, and it can be very useful when you're receiving a hash of data where you don't necessarily know the key-value pairs in advance. 

{% highlight ruby %}
require 'ostruct'

shopping_list = OpenStruct.new({ cheese: 5, apples: 2, bananas: 4})

shopping_list.cheese
=> 5 

shopping_list.bananas
=> 4 

shopping_list.cookies = 7

shopping_list
=> #<OpenStruct cheese=5, apples=2, bananas=4, cookies=7> 
{% endhighlight %}

We can combine OpenStruct with JSON.parse. This will allow us to use method calls as opposed to bracket syntax (data.city.name instead of data["city"]["name"]). 

{% highlight ruby %}
require 'ostruct'
require 'json'
require 'faraday'
response = Faraday.get('http://api.openweathermap.org/data/2.5/forecast?q=Chicago,us&units=imperial&APPID=442eba5b3e3a3ae8ead5698479bcdaa8')
weather_data = JSON.parse(response.body, object_class: OpenStruct)
weather_data.city.name
=> "Chicago"
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Making API Calls and Parsing JSON, Version II</span>
    <p>
      Modify your `weather_forecast.rb` program so that you call methods to retreive data instead of accessing data with hash syntax. 
    </p> 
  </div>
</div>
