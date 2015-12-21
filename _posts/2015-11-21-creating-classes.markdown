---
title: Creating Classes
layout: post
date: 2015-11-21 23:59:49
permalink: creating-classes
---

* what is a class?
* behavior (actions) and attributes
* initialize
* instance variables
* attr_reader, attr_writer, attr_accessor
* private methods
* require_relative

{% highlight ruby %}
class Task
  attr_reader   :title, :description
  attr_accessor :status
  
  def initialize(title, description, status)
    @title       = title
    @description = description
    @status      = status
  end

  def complete!
    complete = "Completed"
  end
end
{% endhighlight %}
