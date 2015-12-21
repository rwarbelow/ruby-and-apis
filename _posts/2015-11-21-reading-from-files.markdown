---
title: Reading from Files
layout: post
date: 2015-11-21 23:59:54
permalink: reading-from-files
---

In this section, we'll learn how to read in text files using the [File](http://ruby-doc.org/core-2.2.0/File.html) class in Ruby. 

* File.open
* #close
* #read
* File.exist? 

{% highlight ruby %}
contents = ''

f = File.open('cheese-ipsum.txt', "r") 

f.each_line do |line|
  contents += line
end

puts contents
{% endhighlight %}


{% highlight ruby %}
File.readlines('cheese-ipsum.txt').each do |line|
  puts line
end
{% endhighlight %}


