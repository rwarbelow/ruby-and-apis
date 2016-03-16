---
title: ActiveRecord and Databases
layout: post
date: 2015-01-04 23:59:51
permalink: activerecord-and-postgres
---

![orm](http://wiki.expertiza.ncsu.edu/images/2/2c/ORM_Flowchart.jpg)

(Diagram courtesy of expertiza.ncsu.edu)

An Object Relational Mapper "translates" between a programming language (Ruby, in our case) and a database.

Let's try out an example. Clone down the [Active Record Practice](https://github.com/rwarbelow/active_record_practice) repo. 

First, we'll look at the setup:

<ul>
  <li>Gemfile</li>
  <li>Rakefile</li>
  <li>config/database.yml</li>
  <li>db/migrate</li>
</ul>

Let's start by creating a database:

```
$ rake db:create
```

This will look at our `config/database.yml` file and create a database with that name. 

#### Migrations

You can access the guides for ActiveRecord [here](http://guides.rubyonrails.org/v3.2.8/migrations.html). 

A migration is a file that can be used to change the structure of your database. We start with an empty database, and we'll need to add a table for whatever we want to store. Later on, we might want to add another table, or remove a column, or change a column type. 

Instead of writing SQL directly in order to change the database structure, we can store these changes in migration files which will allow us to share these changes easily with anyone else on our team. 

Since we've already created a database, we can go ahead and make a migration that we'll use to modify the structure of our empty database. In this case, we're modifying the structure by creating a table. *Table names are always plural.*

```
$ rake db:create_migration NAME=create_people
```

This will generate a file inside of `db/migrate` with a timestamp and the name `add_people`. Go ahead and open that file. 

Inside of the change method, we'll specify what we want to change about the database:

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

Now that we have the code, we'll run it so that it actually creates the table. We do this with the following command:
<div>


```
$ rake db:migrate
```

</div>
This created a file called `schema.rb`. Let's look at it:

{% highlight ruby %}
# lots of comments
# and more comments

ActiveRecord::Schema.define(version: 20160218215147) do

  create_table "people", force: :cascade do |t|
    t.string   "firstname"
    t.string   "lastname"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

end
{% endhighlight %}

The schema is a file that we will not modify by hand. Instead, it acts as a snapshot so that we can easily see what the structure of our database looks like at any given time. 

So that takes care of the database level. Now we need to create Ruby objects that can communicate with the database.

#### Models

Normally, each of our models would live in a separate file. Since this is just a playground, we'll go ahead and define the models inside of the `playground.rb` file. *Model names are always singular.*

{% highlight ruby %}
class Person < ActiveRecord::Base
end
{% endhighlight %}

That's it! By inheriting from ActiveRecord, our Person class will automatically inherit initialize method, in addition to some common methods that we'll use to interact with the database. If we run the file, we'll hit the `pry` and then we'll have an interactive place to play around with ActiveRecord:

```
$ ruby playground.rb
```

Once in the pry session:

{% highlight ruby %}
pry(main)> rachel = Person.create(firstname: "rachel", lastname: "warbelow")
# => #<Person:0x007fbecb2cb938 id: 1, firstname: "rachel", lastname: "warbelow", created_at: 2016-02-01 22:24:54 UTC, updated_at: 2016-02-01 22:24:54 UTC>

pry(main)> Person.all
# => [#<Person:0x007fbecb0320f0 id: 1, firstname: "rachel", lastname: "warbelow", created_at: 2016-02-01 22:24:54 UTC, updated_at: 2016-02-01 22:24:54 UTC>]

pry(main)> Person.count
# => 1

pry(main)> bob = Person.create(firstname: "bob", lastname: "smith")
# => #<Person:0x007fbeccd9f520 id: 2, firstname: "bob", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>

pry(main)> mary = Person.create(firstname: "mary", lastname: "smith")
# => #<Person:0x007fbecce4a518 id: 3, firstname: "mary", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>

# => [#<Person:0x007fbeccd451b0 id: 1, firstname: "rachel", lastname: "warbelow", created_at: 2016-02-01 22:24:54 UTC, updated_at: 2016-02-01 22:24:54 UTC>,
 #<Person:0x007fbeccd45020 id: 2, firstname: "bob", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>, #<Person:0x007fbecce4a518 id: 3, firstname: "mary", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>]

pry(main)> Person.count
# => 3
{% endhighlight %}

We can also access methods on the instance of each of our people:

{% highlight ruby %}
pry(main)> rachel.firstname
# => "rachel"

pry(main)> bob.lastname
# => "smith"

pry(main)> bob.update(firstname: "bobby")
pry(main)> bob
# => #<Person:0x007fbeccd9f520 id: 2, firstname: "bobby", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:33:27 UTC>
{% endhighlight %}

In a web app with simple CRUD functionality, here are some helpful methods:

{% highlight ruby %}
pry(main)> Person.where(last_name: "smith")

# => [#<Person:0x007fbeccd45020 id: 2, firstname: "bob", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>, #<Person:0x007fbecce4a518 id: 3, firstname: "mary", lastname: "smith", created_at: 2016-02-01 22:27:45 UTC, updated_at: 2016-02-01 22:27:45 UTC>]

pry(main)> person_one = Person.find(1)
# => #<Person:0x007fbeccc561a0 id: 1, firstname: "rachel", lastname: "warbelow", created_at: 2016-02-01 22:24:54 UTC, updated_at: 2016-02-01 22:24:54 UTC>

pry(main)> person_one.destroy
=> #<Person:0x007fbeccc561a0 id: 1, firstname: "rachel", lastname: "warbelow", created_at: 2016-02-01 22:24:54 UTC, updated_at: 2016-02-01 22:24:54 UTC>
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Interacting with a Database using ActiveRecord</span>
    <p>
      First, type `git reset --hard`. This will erase all of the work we've done so far so that you have a fresh slate.
    </p>
    <p>
      Create a migration for tasks. A task has a title and a description. It also should have a priority level (1-5). 
    </p>
    <p>In pry, create some tasks. Make sure that at least two of them have the same priority level.</p>
    <ul>
      <li>Find the task with the id of 3.</li>
      <li>Find a task with a specific title.</li>
      <li>Find all tasks that have a specific priority level.</li>
      <li>Count all of your tasks.</li>
      <li>Return the collection of all of your tasks.</li>
      <li>Update the description of one of your tasks.</li>
    </ul>
  </div>
</div>
