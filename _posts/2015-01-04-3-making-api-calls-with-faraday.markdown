---
title: Making API Calls with Faraday
layout: post
date: 2015-01-04 23:59:57
permalink: api-calls-with-faraday
---

<a href="https://github.com/lostisland/faraday">Faraday</a> is a Ruby Gem that can be used to make HTTP requests. It provides a simpler interface over the built-in Ruby HTTP client. 

To install a gem in Ruby, we type `gem install faraday` on the command line. This will put the source code on our machine.

Then in irb:

{% highlight ruby %}
require 'faraday'
Faraday.get('http://www.example.com')
{% endhighlight %}

Faraday is helpful when fetching API data, too. Notice that I've appended `APPID=442eba5b3e3a3ae8ead5698479bcdaa8` to the end of the call as a query string. This is a key that is given when registering with <a href="http://openweathermap.org/">OpenWeatherMap</a>

{% highlight ruby %}
require 'faraday'
response = Faraday.get('http://api.openweathermap.org/data/2.5/forecast?q=Chicago,us&units=imperial&APPID=442eba5b3e3a3ae8ead5698479bcdaa8')
puts response.body
{% endhighlight %}

You can find the format of the JSON response on the <a href="http://openweathermap.org/forecast5">OpenWeatherMap Forecast Documentation</a>.

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Making API Calls and Parsing JSON</span>
    <p>
      Write a program `weather_forecast.rb` that accept a command-line argument for a city and returns a list like this:
    </p> <br>
    <p>
2016-01-08 06:00:00 -- 34.7 degrees <br>
2016-01-08 09:00:00 -- 32.1 degrees <br>
...etc
    </p> <br>
      <p>
      Once you have the parsed response, you'll want to iterate: parsed_response.list.each do |data|...
    </p>

  </div>
</div>
