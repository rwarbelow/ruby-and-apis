---
title: Writing to Files
layout: post
date: 2015-11-21 23:59:53
permalink: writing-to-files
---

In this section, we'll use the [File](http://ruby-doc.org/core-2.2.0/File.html) class in order to write to new files, append to existing files, and overwrite existing files. We'll also learn about additional modes that can be passed into the `File.open` method. 

* read only ("r")
* write only ("w")
* append only ("a")
* read-write permission for appending ("a+")

* ('myfile.txt', 'r+'), ('myfile.txt', 'w+')

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}
