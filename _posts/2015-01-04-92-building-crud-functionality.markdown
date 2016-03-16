---
title: Building CRUD Functionality
layout: post
date: 2015-01-04 23:59:48
permalink: building-crud-functionality
---

### Creating People

Let's add a way to create people. In the `index.erb`:

{% highlight html %}
<h1>All People</h1>

<ul>
  <% @people.each do |person| %>
    <li><%= person.first_name %> <%= person.last_name %> </li>
  <% end %>
</ul>

<a href="/people/new">Add New Person</a>
{% endhighlight %}

We've linked to this route, but we need to add an endpoint for it in our controller:

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = Person.all
    erb(:index)
  end

  get '/people/new' do
    erb(:new)
  end
end
{% endhighlight %}

Now that we've told it to render the `:new` erb file, we need to make that inside of `views`:

```
$ touch app/views/new.erb
```

Inside of that file:

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

Our form action is `'/people'` with a method of `POST`. We'll need to add this endpoint in the controller as well:

{% highlight ruby %}
require 'sinatra'

class PeopleDatabaseApp < Sinatra::Base
  get '/' do
    "Hello, world!"
  end

  get '/people' do
    @people = Person.all
    erb(:index)
  end

  get '/people/new' do
    erb(:new)
  end

  post '/people' do
    Person.create(params[:person])
    redirect '/people'
  end
end
{% endhighlight %}

### Editing People

We'll first modify our index to include an edit link next to each individual person. When we click this link, we want it to bring us to a form to edit the individual person: 

{% highlight html %}
<h1>All People</h1>

<ul>
  <% @people.each do |person| %>
    <li>
      <%= person.firstname %> <%= person.lastname %> <a href="/people/<%= person.id %>/edit">Edit</a>
    </li>
  <% end %>
</ul>

<a href="/people/new">Add New Person</a>
{% endhighlight %}

Next, we'll add this route in our controller:

{% highlight ruby %}
class Application < Sinatra::Base
  get '/' do
    erb :dashboard
  end

  get '/people' do
    @people = Person.all
    erb :index
  end

  get '/people/new' do
    erb :new
  end

  post '/people' do
    Person.create(params[:person])
    redirect '/people'
  end

  get '/people/:id/edit' do |id|
    @person = Person.find(id.to_i)
    erb :edit
  end
end
{% endhighlight %}

Now create the `edit` template:

```
$ touch app/views/edit.erb
```

And make a form to edit the existing person:

{% highlight html %}
<h1>Edit</h1>
<form action="/people/<%= @person.id %>" method="post">
  <input type="hidden" name="_method" value="PUT" />
  <input type='text' name='person[firstname]' value="<%= @person.firstname %>"/><br/>
  <input type='text' name='person[lastname]' value="<%= @person.lastname %>"/><br/>
  <input type='submit'/>
</form>
{% endhighlight %}

Notice that we've embedded the id of the person in the URL. This is so we can determine which person we are updating when we hit submit. Now let's add an endpoint for this form submission in our controller:

{% highlight ruby %}
class Application < Sinatra::Base
  set :method_override, true

  get '/' do
    erb :dashboard
  end

  get '/people' do
    @people = Person.all
    erb :index
  end

  get '/people/new' do
    erb :new
  end

  post '/people' do
    Person.create(params[:person])
    redirect '/people'
  end

  get '/people/:id/edit' do |id|
    @person = Person.find(id.to_i)
    erb :edit
  end

  put '/people/:id' do |id|
    Person.update(id, params[:person])
    redirect '/people'
  end
end
{% endhighlight %}

### Deleting People

First, add a button to delete a person in the index:

{% highlight html %}
<h1>All People</h1>

<ul>
  <% @people.each do |person| %>
    <li>
      <%= person.firstname %> <%= person.lastname %> <a href="/people/<%= person.id %>/edit">Edit</a>
      <form action="/people/<%= person.id %>" method="POST">
        <input type="hidden" name="_method" value="DELETE">
        <input type="submit" value="delete"/>
      </form>
    </li>
  <% end %>
</ul>

<a href="/people/new">Add New Person</a>
{% endhighlight %}

Then add an endpoint in the controller:

{% highlight ruby %}
class Application < Sinatra::Base
  set :method_override, true

  get '/' do
    erb :dashboard
  end

  get '/people' do
    @people = Person.all
    erb :index
  end

  get '/people/new' do
    erb :new
  end

  post '/people' do
    Person.create(params[:person])
    redirect '/people'
  end

  get '/people/:id/edit' do |id|
    @person = Person.find(id.to_i)
    erb :edit
  end

  put '/people/:id' do |id|
    Person.update(id, params[:person])
    redirect '/people'
  end

  delete '/people/:id' do |id|
    Person.delete(id)
    redirect '/people'
  end
end
{% endhighlight %}

Now let's add, commit, and push our work to Heroku!

```
$ git add .
$ git commit -m 'build out CRUD functionality'
$ git push heroku master
```

We do not need to migrate on Heroku again since we did not create any new migration files (ie -- modify the database structure in some way). 

Navigate to your app in your browser and check it out! 