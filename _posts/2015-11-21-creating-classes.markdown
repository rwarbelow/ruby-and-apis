---
title: Creating Classes
layout: post
date: 2015-11-21 23:59:49
permalink: creating-classes
---

<h4>What is a Class?</h4>

A class is what is used to define an object that has behavior and attributes. We've already seen built-in classes in Ruby: String, Array, Hash, Integer, etc. These classes are all objects with their own behavior and attributes. For example, it wouldn't make sense to call `#capitalize` on an object of type Integer. 

<h4>Naming Conventions</h4>

Unlike variable naming, we use CamelCase for naming classes:

{% highlight ruby %}
class Person
end

class StudentTeacher
end
{% endhighlight %}

<h4>Attributes</h4>

Objects generally will have attributes that contain some type of data specific to that instance. These attributes are stored as instance variables (`@attribute`) upon initialization of a new object. Let's look at the example below:

{% highlight ruby %}
class Task
  def initialize(title, description, status)
    @title       = title
    @description = description
    @status      = status
  end
end
{% endhighlight %}

We can use these instance variables in any other method that we define in the class. We can also create a getter and/or setter method for each of these variables using an attr_reader, attr_accessor, or attr_writer:

{% highlight ruby %}
class Task
  attr_reader   :title, :description
  attr_accessor :status

  def initialize(title, description, status)
    @title       = title
    @description = description
    @status      = status
  end
end
{% endhighlight %}

This allows us to do the following:

{% highlight ruby %}
task = Task.new("Buy ticket", "DEN -> NYC", "Incomplete")
task.title #=> "Buy ticket"
task.description #=> "DEN -> NYC"
task.status #=> "Incomplete"
{% endhighlight %}

<h4>Behavior</h4>

Behavior of an object is encapsulated in its methods. For example, completing a task would be an action or behavior. Asking whether or not the task is complete would also be an action. 

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
    status = "Complete"
  end

  def complete?
    status == "Complete"
  end
end
{% endhighlight %}

<h4>Initializing an Object</h4>

Now that we've defined the class, we can create new instances of the object and call its methods:

{% highlight ruby %}
task = Task.new("Buy ticket", "DEN -> NYC", "Incomplete")
task.complete? #=> false
task.complete!
task.complete? #=> true
{% endhighlight %}

Data passed into the initialize method can also come through as a hash. This is more flexible since the order of the data does not matter. 

{% highlight ruby %}
class Task
  attr_reader   :title, :description
  attr_accessor :status
  
  def initialize(data)
    @title       = data[:title]
    @description = data[:description]
    @status      = data[:status]
  end

  def complete!
    complete = "Complete"
  end

  def complete?
    status == "Complete"
  end
end
{% endhighlight %}

{% highlight ruby %}
task = Task.new({ title: "Buy ticket", description: "DEN -> NYC", status: "Incomplete" })

# OR

task = Task.new(title: "Buy ticket", description: "DEN -> NYC", status: "Incomplete")

# OR
data = { title: "Buy ticket", description: "DEN -> NYC", status: "Incomplete" }
task = Task.new(data)
{% endhighlight %}

Iterate through the collection of hashes below and return an array that holds instances of `Person` objects:

{% highlight ruby %}
raw_data = [{:first_name=>"Nancy", :last_name=>"Gonzalez", :email=>"ngonzalez0@mtv.com", :state=>"Florida"}, 
            {:first_name=>"Theresa", :last_name=>"Kim", :email=>"tkim1@chron.com", :state=>"Florida"}, 
            {:first_name=>"Ronald", :last_name=>"Roberts", :email=>"rroberts2@reddit.com", :state=>"Washington"}, 
            {:first_name=>"Helen", :last_name=>"Stephens", :email=>"hstephens3@thetimes.co.uk", :state=>"California"}, 
            {:first_name=>"Julie", :last_name=>"Hughes", :email=>"jhughes4@ucsd.edu", :state=>"New York"}, 
            {:first_name=>"Andrew", :last_name=>"Cook", :email=>"acook5@booking.com", :state=>"Utah"}, 
            {:first_name=>"Fred", :last_name=>"Richardson", :email=>"frichardson6@deliciousdays.com", :state=>"Texas"}, 
            {:first_name=>"Harold", :last_name=>"Rivera", :email=>"hrivera7@who.int", :state=>"New Jersey"}, 
            {:first_name=>"Betty", :last_name=>"Patterson", :email=>"bpatterson8@blogger.com", :state=>"Florida"}, 
            {:first_name=>"Fred", :last_name=>"Jackson", :email=>"fjackson9@blogger.com", :state=>"Georgia"}, 
            {:first_name=>"Anne", :last_name=>"Carpenter", :email=>"acarpentera@upenn.edu", :state=>"Florida"}, 
            {:first_name=>"Lillian", :last_name=>"Robinson", :email=>"lrobinsonb@cloudflare.com", :state=>"Wisconsin"}, 
            {:first_name=>"Ashley", :last_name=>"Grant", :email=>"agrantc@trellian.com", :state=>"California"}, 
            {:first_name=>"Bobby", :last_name=>"Rose", :email=>"brosed@baidu.com", :state=>"District of Columbia"}, 
            {:first_name=>"Timothy", :last_name=>"Castillo", :email=>"tcastilloe@yelp.com", :state=>"California"}]

people = # Your code here. This variable should be an array of Person objects. 
{% endhighlight %}

<h4>Classes Interacting</h4>

Now, let's create a `PeopleDatabase` class that holds all of our people. Upon initialization, it will accept an array of Person objects:

{% highlight ruby %}
class PeopleDatabase
  attr_reader :people
  def initialize(people)
    @people = people
  end
end
{% endhighlight %}

What sorts of things would we want the PeopleDatabase to do? 

Let's start by being able to add a new person to the collection:

{% highlight ruby %}
class PeopleDatabase
  attr_reader :people
  def initialize(people)
    @people = people
  end

  def add_person(data)
    person = Person.new(data)
    people << person
  end
end
{% endhighlight %}

We can use `require 'pry'; binding.pry` at the bottom of our file in order to easily interact with our PeopleDatabase.

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Adding PeopleDatabase Functionality</span>
    <p>
      Add functionality so that `PeopleDatabase` can:
      <li>Remove a person from the collection given an email address</li>
      <li>Return all of the people from a given state</li>
      <li>Return a comma-separated string of every person's email address</li>
      <li>Count the number of people from a given state</li>
    </p> <br>
    <p>
      It's perfectly OK to look at the Ruby docs or StackOverflow answers!
    </p>
  </div>
</div>

<h4>Organizing our Files</h4>

It is conventional to separate each class into it's own file. For this reason, let's create `person.rb` and `people_database.rb`. Let's also create our executable file and call it `people_database_runner.rb`. Since we no longer have defined `Person` and `PeopleDatabase` in the same file, we'll need to use `require_relative`. 

{% highlight ruby %}
require 'csv'
require_relative 'person'  # use the name of the file without the extension
require_relative 'people_database'

raw_data = [{:first_name=>"Nancy", :last_name=>"Gonzalez", :email=>"ngonzalez0@mtv.com", :state=>"Florida"}, 
            {:first_name=>"Theresa", :last_name=>"Kim", :email=>"tkim1@chron.com", :state=>"Florida"}, 
            {:first_name=>"Ronald", :last_name=>"Roberts", :email=>"rroberts2@reddit.com", :state=>"Washington"}, 
            {:first_name=>"Helen", :last_name=>"Stephens", :email=>"hstephens3@thetimes.co.uk", :state=>"California"}, 
            {:first_name=>"Julie", :last_name=>"Hughes", :email=>"jhughes4@ucsd.edu", :state=>"New York"}, 
            {:first_name=>"Andrew", :last_name=>"Cook", :email=>"acook5@booking.com", :state=>"Utah"}, 
            {:first_name=>"Fred", :last_name=>"Richardson", :email=>"frichardson6@deliciousdays.com", :state=>"Texas"}, 
            {:first_name=>"Harold", :last_name=>"Rivera", :email=>"hrivera7@who.int", :state=>"New Jersey"}, 
            {:first_name=>"Betty", :last_name=>"Patterson", :email=>"bpatterson8@blogger.com", :state=>"Florida"}, 
            {:first_name=>"Fred", :last_name=>"Jackson", :email=>"fjackson9@blogger.com", :state=>"Georgia"}, 
            {:first_name=>"Anne", :last_name=>"Carpenter", :email=>"acarpentera@upenn.edu", :state=>"Florida"}, 
            {:first_name=>"Lillian", :last_name=>"Robinson", :email=>"lrobinsonb@cloudflare.com", :state=>"Wisconsin"}, 
            {:first_name=>"Ashley", :last_name=>"Grant", :email=>"agrantc@trellian.com", :state=>"California"}, 
            {:first_name=>"Bobby", :last_name=>"Rose", :email=>"brosed@baidu.com", :state=>"District of Columbia"}, 
            {:first_name=>"Timothy", :last_name=>"Castillo", :email=>"tcastilloe@yelp.com", :state=>"California"}]

people = raw_data.map { |row| Person.new(row) }

people_db = PeopleDatabase.new(people)

require 'pry'; binding.pry
{% endhighlight %}
