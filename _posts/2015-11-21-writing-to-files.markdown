---
title: Writing to Files
layout: post
date: 2015-11-21 23:59:53
permalink: writing-to-files
---

In this section, we'll use the [File](http://ruby-doc.org/core-2.2.0/File.html) class in order to write to new files, append to existing files, and overwrite existing files. We'll also learn about additional modes that can be passed into the `File.open` method. 

To write to a file, we open a file in "write" mode. This mode is indicated by `"w"` as the second argument. WARNING: Write mode will overwrite anything already existing in the file. The two examples below will have the same effect. 

{% highlight ruby %}
file = File.open("write-example.txt", "w")
file.puts "Hello, world!"
file.puts "Here's another line."
file.close
{% endhighlight %}

{% highlight ruby %}
File.open("write-example.txt", "w") do |file| 
  file.puts "Hello, world!"
  file.puts "Here's another line."
end
# this will automatically close the file handler for you
{% endhighlight %}

If you want to be able to read and write to the file, use the mode `"r+"`. This will allow you to write to the file. Where you write to depends on where the position is at that moment. It will overwrite what already exists in those specific position numbers, but it will not overwrite the whole file.

Let's try it in irb:

{% highlight ruby %}
file = File.open("example.txt", "r+")
file.read
file.puts "hello"
file.rewind
file.puts "hello"
file.rewind
file.read
{% endhighlight %}

What happened in the above example? 

To read and append to the file, use the mode `"a+"`.

{% highlight ruby %}
file = File.open("example.txt", "a+")
file.read
file.puts "hello"
file.rewind
file.puts "hello"
file.rewind
file.read
{% endhighlight %}

What happened in the above example? How is it different from the previous example? 

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Writing gifts to a file</span>
    <p>
      Open your gift list program. When the user wants to quit, save the gifts to a file. The user should be able to run the program multiple times without overwriting existing gifts. 
    </p> <br>
    <p>
      BONUS #1: Sort the gifts from the most asked for gift to the least asked for gift. Use the `#sort_by` method on your gifts hash.
    </p> <br>
    <p>
      BONUS #2: Add a number in front of each gift:
      <li>1. Warm socks</li>
      <li>2. Lamborghini</li>
      <li>...etc...</li>
    </p>
  </div>
</div>
