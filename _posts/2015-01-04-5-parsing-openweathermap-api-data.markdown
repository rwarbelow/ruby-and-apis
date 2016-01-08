---
title: Interacting with the OpenWeatherMap API through Ruby
layout: post
date: 2015-01-04 23:59:55
permalink: openweathermap-api
---

`config.yml`:
{% highlight yaml %}
API_KEY:
  442eba5b3e3a3ae8ead5698479bcdaa8
{% endhighlight %}

`weather_forecast.rb`:
{% highlight ruby %}
require_relative 'weather'
require_relative 'forecast'
require 'optparse'

options = {}

parser = OptionParser.new do|opts|
  opts.on('-c', '--city city', 'City') do |city|
    options[:city] = city;
  end
end

parser.parse!

forecasts = Weather.for("Chicago")

forecasts.each do |forecast|
  puts "#{forecast.datetime} -- #{forecast.temp} degrees: #{forecast.description}"  
end
{% endhighlight %}

`weather.rb`:
{% highlight ruby %}
require 'faraday'
require 'json'
require 'ostruct'
require 'yaml'
require 'date'

API_KEY = YAML.load_file("config.yml")["API_KEY"]
API_URL = "http://api.openweathermap.org/data/2.5"

class Weather
  def self.for(city)
    raw_data = Faraday.get("#{API_URL}/forecast?q=#{city},us&units=imperial&APPID=#{API_KEY}").body
    weather_data = JSON.parse(raw_data, object_class: OpenStruct)
    weather_data.list.map do |data|
      Forecast.new(data)
    end
  end
end
{% endhighlight %}

`forecast.rb`:
{% highlight ruby %}

class Forecast
  attr_reader :datetime, :temp, :description
  def initialize(data)
    @datetime    = data.dt_txt
    @temp        = data.main.temp
    @description = data.weather.first.description
  end
end
{% endhighlight %}