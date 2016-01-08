---
title: Configuration with YAML Files
layout: post
date: 2015-01-04 23:59:58
permalink: configuration-with-yaml
---

YAML stands for "YAML Ain't Markup Language" and is a human- and machine-readable data format. Let's try a few experiments:

Make a file called `example.yml`. Inside of that file, paste this:

{% highlight yaml %}
username:
  myname
password:
  mysecretpassword
{% endhighlight %}

Then go into irb:

{% highlight ruby %}
data = YAML.load_file("example.yml")
=> {"username"=>"myname", "password"=>"mysecretpassword"} 
data["username"]
=> "myname"
data["password"]
=> mysecretpassword
{% endhighlight %}

YAML is not just for storing string keys and values. You can store an array as the value like this:

{% highlight yaml %}
locations: 
  - Denver
  - Boulder
  - Colorado Springs
{% endhighlight %}

Then in irb:

{% highlight ruby %}
data = YAML.load_file("example.yml")
=> {"locations"=>["Denver", "Boulder", "Colorado Springs"]} 
{% endhighlight %}

In a program where you don't want to save your username and password in the source code, you might try something like this:

{% highlight yaml %}
username:
  rachel
password:
  mysecretpassword
{% endhighlight %}

{% highlight ruby %}
require 'yaml'
config = YAML.load_file('config.yml')
username = config['username']
password = config['password']
{% endhighlight %}

By doing this, you'll be able to share the source code without sharing usernames and passwords.   

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Using A YAML file to access configurations</span>
    <p>
      First, set an environment variable for your Terminal session:
    </p>
    <p>
      {% highlight css %}
      $ export SECRET_PASSWORD=mysecretpassword
      {% endhighlight %}
    </p> <br>
    <p>
      Next, create a config.yml file where you'll store a username and password. 
    </p> <br>
    <p>
{% highlight css %}
username:
  yournamehere
password:
  yourpasswordhere
{% endhighlight %}
    </p>
    <p>
      Then, modify your gift list program to not run unless the password in the config file matches the exported secret password. In Ruby, environment variables can be accessed like this:
    </p> <br>
    <p>
{% highlight ruby %}
ENV["SECRET_PASSWORD"]
{% endhighlight %}
    </p>
  </div>
</div>
