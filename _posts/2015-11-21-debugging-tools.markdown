---
title: Debugging Tools
layout: post
date: 2015-11-21 23:59:58
permalink: debugging-tools
---

In this section, we'll take a look at a few ways to debug Ruby code, including `puts` and a Ruby gem called `pry`.

#### `puts` or `p`

{% highlight ruby %}

2.2.2 :001 > percentage = 0.75 * 100
           => 75.0 
2.2.2 :002 > puts percentage
           75.0
           => nil 
2.2.2 :003 > p percentage
           75.0
           => 75.0 

{% endhighlight %}

{% highlight ruby %}
2.2.2 :001 > animals = ["cat", "dog", "raven"]
           => ["cat", "dog", "raven"] 
2.2.2 :002 > puts animals
           cat
           dog
           raven
           => nil 
2.2.2 :003 > p animals
           ["cat", "dog", "raven"]
           => ["cat", "dog", "raven"]
{% endhighlight %}

#### `pry`
* pseudocode
