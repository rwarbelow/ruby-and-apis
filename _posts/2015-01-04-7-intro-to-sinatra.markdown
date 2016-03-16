---
title: Intro to Sinatra
layout: post
date: 2015-01-04 23:59:53
permalink: intro-to-sinatra
---

Sinatra is a domain-specific language that allows easy access to making a Ruby web application. 

### Review: How the Web Works

Let's diagram a very basic client-server model and figure out where Sinatra comes into play. 

### Up and Running

Let's set up our first Sinatra web application. We'll take our PeopleDatabase concept and move it to the web. First, make a directory for your project and change into that directory:

```
$ mkdir people_database
$ cd people_database
```

Then, we'll need an app file, a Gemfile, and a config file:

```
$ touch app.rb
$ touch config.ru
$ touch Gemfile
```

Open the whole project inside of your text editor. 

### The Gemfile

The Gemfile is where we define which Ruby libraries (or "gems") our project depends on. Inside `Gemfile`, add the following:

{% highlight ruby %}
source 'https://rubygems.org'

gem 'sinatra', require: 'sinatra/base'
gem 'shotgun'
{% endhighlight %}

In order to install these gems, and to generate a `Gemfile.lock` (which keeps track of Gem versions), we'll need to bundle. From the command line:

```
$ gem install bundler
$ bundle
```

Let's take a look at what was generated in the `Gemfile.lock`. 

### The Config File

The `config.ru` file will tell the webserver how to run our app.

{% highlight ruby %}
require File.expand_path('../app',  __FILE__)

run PeopleDatabaseApp
{% endhighlight %}

### The App File

The `app.rb` file will be where we define our available routes (like "http://localhost:9393/" or "http://localhost:9393/people" or "http://localhost:9393/people/new", etc.). 

To set up the most basic version of this file, add the following to `app.rb`:

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end
end
{% endhighlight %}

Now we have a very basic web app! Let's start it up and take a look in the browser.

```
$ shotgun
```

Now navigate to `http://localhost:9393/`. 
