---
title: Building Routes and Views in Sinatra
layout: post
date: 2015-01-04 23:59:52
permalink: building-routes-and-views-in-sinatra
---

Now let's add some other routes. 

### Adding a index of all people at `/people`

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = ["John", "Emily", "Rachel", "Harrison", "Jim"]
  end
end
{% endhighlight %}

If you navigate to `http://localhost:9393/people`, you'll see all of us, but it's not very beautifully styled. Ultimately, we want to create an HTML view that looks like this:

<ul>
  <li>John</li>
  <li>Emily</li>
  <li>Rachel</li>
  <li>Harrison</li>
  <li>Jim</li>
</ul>

So this is where we'll need to add in views. Go ahead and create a views folder and a people index from the command line:

```
$ mkdir views
$ touch views/index.erb
```

This `index.erb` file will allow us to create an HTML document with embedded Ruby (erb). 

Now let's tell our app file to render the index template:

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = ["John", "Emily", "Rachel", "Harrison", "Jim"]
    erb(:index)
  end
end
{% endhighlight %}

Inside of an `.erb` file, we have to use special tags in order to indicate where Ruby lives and distinguish that from plain HTML.

{% highlight html %}
<h1>All People</h1>

<ul>
  <% @people.each do |person| %>
    <li><%= person %></li>
  <% end %>
</ul>
{% endhighlight %}

Now refresh the page. Tada! 

### Form for a New Person

We want users of our app to be able to submit new people to the PeopleDatabase. In order to do this, we'll need a new route and a form for that route:

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = ["John", "Emily", "Rachel", "Harrison", "Jim"]
    erb(:index)
  end

  get '/people/new' do
    erb(:new)
  end
end
{% endhighlight %}


{% highlight html %}
<h1>New Person</h1>

<form action="/people" method="POST">
  <label for="person[firstname]">First Name</label>
  <input type="text" name="person[firstname]">
  <label for="person[lastname]">Last Name</label>
  <input type="text" name="person[lastname]">
  <input type="submit">
</form>
{% endhighlight %}

Notice that when we hit the submit button, we get an error. Let's figure out what this error means, then we'll add the appropriate route. First, add our debugging tool, `pry`, to your Gemfile: 

{% highlight ruby %}
source 'https://rubygems.org'

gem 'sinatra', require: 'sinatra/base'
gem 'shotgun'
gem 'pry'
{% endhighlight %}

Then bundle:

```
$ bundle
```

In your PeopleDatabaseApp file, add the following route: 

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = ["John", "Emily", "Rachel", "Harrison", "Jim"]
    erb(:index)
  end

  get '/people/new' do
    erb(:new)
  end

  post '/people' do
    require 'pry'; binding.pry
  end
end
{% endhighlight %}

Start up your server again (`shotgun`), navigate to `http://localhost:9393/people/new`, and submit some data. Now navigate back to your server log and we can play around. 

If you type `params`, you'll see this:

{% highlight ruby %}
{"person"=>{"firstname"=>"rachel", "lastname"=>"warbelow"}}
{% endhighlight %}

This is great! We can get the first name and last name values by typing `params["person"]`. But now we've run into a problem... since HTTP is stateless, and we don't have a database, we can't save this information anywhere. 

We'll put our web app to the side for now in order to talk about how we can use Ruby to communicate with a database. 