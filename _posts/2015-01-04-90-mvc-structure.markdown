---
title: MVC Structure
layout: post
date: 2015-01-04 23:59:50
permalink: mvc-structure
---

MVC is a software architecture pattern that is built into Rails and we can mimick in Sinatra. 

Here's a diagram of MVC from Adventured.co:

![mvc](http://www.adventured.co/wp-content/uploads/2015/06/ruby-on-rails-architecture-01-mvc-architecture-best-ideas-lesson-01-the-mvc-architecture-for-ruby-on-rails.jpg)

We'll start by cloning down an ActiveRecord Sinatra starter repo. This will be our "starter kit" for any Sinatra web app that needs a database. 

Find the repository [here](https://github.com/rwarbelow/sinatra_starter). Once you have it cloned down (`git clone http://github.com/rwarbelow/sinatra_starter`), run `bundle` to install all of the necessary gems. We'll start by walking through the folders and files:

<ul>
  <li>Gemfile</li>
  <li>Rakefile</li>
  <li>app/controllers</li>
  <li>app/models</li>
  <li>app/views</li>
  <li>config/database.yml</li>
  <li>config/database.rb</li>
  <li>config/environment.rb</li>
</ul>

Let's transfer over some of the functionality from our PeopleDatabase app. First, we'll need a database.

```
$ rake db:create
```

And we'll need table in our database:

```
$ rake db:create_migration NAME=create_people
```

Inside of that migration file, define the method that will create the people table:

{% highlight ruby %}
class CreatePeople < ActiveRecord::Migration
  def change
    create_table :people do |t|
      t.string :firstname
      t.string :lastname
      
      t.timestamps
    end
  end
end
{% endhighlight %}

Go ahead and migrate. 

```
$ rake db:migrate
```

And look at your schema:

{% highlight ruby %}
# some comments

ActiveRecord::Schema.define(version: 20160204213811) do

  # These are extensions that must be enabled in order to support this database
  enable_extension "plpgsql"

  create_table "people", force: :cascade do |t|
    t.string   "firstname"
    t.string   "lastname"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

end
{% endhighlight %}

Looks good! Now we'll need a model so that we can use Ruby to access this table in our database.

```
$ touch app/models/person.rb
```

We'll define the class and inherit from ActiveRecord:

{% highlight ruby %}
class Person < ActiveRecord::Base
end
{% endhighlight %}

Now let's add a route for showing all people. In `app/controllers/application.rb`:

{% highlight ruby %}
class Application < Sinatra::Base
  get '/' do
    erb :dashboard
  end

  get '/people' do
    @people = Person.all # remember that the class name is singular
    erb :index
  end
end
{% endhighlight %}

Now we'll need to make an `index.erb` file:

```
$ touch app/views/index.erb
```

And inside of that file:

{% highlight html %}
<h1>All People</h1>

<ul>
  <% @people.each do |person| %>
    <li><%= person.firstname %> <%= person.lastname %></li>
  <% end %>
</ul>
{% endhighlight %}

This file looks a little different from our previous version. This is because we are now passing in actual Person objects that have attributes, so we need to call those attributes in order to see the values. 

Let's see if it works. Start up your server ($ shotgun) and navigate to `http://localhost:9393/people`. You should see the heading "All People" but no people since we don't have any people in our database. That's ok!

We can add some people in a very similar way to what we did with pry in the previous section. Shut down your server by pressing `control + c`. 

We'll use the gem `tux` to access a console where we can create people.

```
$ tux
Loading development environment (Rack 1.3)
>> Person.create(firstname: "rachel", lastname: "warbelow")
>> Person.create(firstname: "bob", lastname: "smith")
>> Person.create(firstname: "mary", lastname: "smith")
>> exit
```

Now start up the server again (`shotgun`) and navigate to `http://localhost:9393/people`. 