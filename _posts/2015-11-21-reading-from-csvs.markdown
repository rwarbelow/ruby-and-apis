---
title: Reading from CSVs
layout: post
date: 2015-11-21 23:59:51
permalink: reading-from-csvs
---

In this section, we'll use the [CSV](http://ruby-doc.org/stdlib-2.2.2/libdoc/csv/rdoc/CSV.html) class from Ruby's standard library in order to read in comma-separated values of CSV files. We'll also learn how to use the first row as headers and convert string headers to symbols.

Go ahead and create a file `people.csv` and add this data:

```
first_name,last_name,email,state
Nancy,Gonzalez,ngonzalez0@mtv.com,Florida
Theresa,Kim,tkim1@chron.com,Florida
Ronald,Roberts,rroberts2@reddit.com,Washington
Helen,Stephens,hstephens3@thetimes.co.uk,California
Julie,Hughes,jhughes4@ucsd.edu,New York
Andrew,Cook,acook5@booking.com,Utah
Fred,Richardson,frichardson6@deliciousdays.com,Texas
Harold,Rivera,hrivera7@who.int,New Jersey
Betty,Patterson,bpatterson8@blogger.com,Florida
Fred,Jackson,fjackson9@blogger.com,Georgia
Anne,Carpenter,acarpentera@upenn.edu,Florida
Lillian,Robinson,lrobinsonb@cloudflare.com,Wisconsin
Ashley,Grant,agrantc@trellian.com,California
Bobby,Rose,brosed@baidu.com,District of Columbia
Timothy,Castillo,tcastilloe@yelp.com,California
```

Let's play around in `irb` first to see what we're doing. Since CSV is not part of the Ruby core library, we need to require it. If we forget this step, we'll see an error `Uninitialized Constant: CSV`.

{% highlight ruby %}
require 'csv'
{% endhighlight %}

Then we can create a Ruby handler for the CSV file:

{% highlight ruby %}
people = CSV.read('people.csv', 'r')
{% endhighlight %}

This returns to us an array of arrays, but if you look at the first inner array, it's just the headers. 

{% highlight ruby %}
people = CSV.read('people.csv', 'r', headers: true)
{% endhighlight %}

This returns to us a `CSV::Table` object. We can iterate through this CSV object:

{% highlight ruby %}
people.each do |person|
  p person
end
{% endhighlight %}

`person` in this case is a `CSV::Row` object. We can access individual pieces of data using hash syntax:

{% highlight ruby %}
people.each do |person|
  p person["first_name"]
end
{% endhighlight %}

If you would prefer to access the data via symbols instead of strings, we can do that:

{% highlight ruby %}
people = CSV.read('people.csv', 'r', headers: true, header_converters: :symbol)
people.each do |person|
  p person[:first_name]
end
{% endhighlight %}

You can also turn these `CSV::Row` objects into actual hashes:

{% highlight ruby %}
people = CSV.read('people.csv', 'r', headers: true, header_converters: :symbol)
people.each do |person|
  p person.to_h
end
{% endhighlight %}

The `.read` method is not the best when you have a gigantic file. Instead, try the `.for_each` method:

{% highlight ruby %}
CSV.foreach('people.csv', headers: true, header_converters: :symbol) do |row|
  p row.to_h
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Reading CSV data to find the average score</span>
    <p>
      Make a file `students.csv` from the data below. Make a ruby file `parser.rb`. Use command-line arguments to accept a file name to parse, then output the average score for the students.
    </p> <br>
    <p>
      BONUS: Report the average score per grade level. What was the average for 9th grade? 10th? 11th? 12th?
    </p>
  </div>
</div>

```
first_name,last_name,grade_level,score
Sarah,Chapman,11,92
Wayne,Gordon,9,86
Bonnie,Harvey,12,70
Cheryl,Wells,10,59
Pamela,Matthews,12,85
Ryan,Mitchell,12,80
Gary,Scott,11,60
Jessica,Ellis,9,93
Carl,Matthews,9,91
Doris,Reynolds,9,56
Marie,Gutierrez,12,81
Andrew,Mills,10,83
Kathy,Hudson,12,77
Walter,Elliott,9,55
Wanda,Harvey,11,97
Ryan,Ruiz,10,65
Lori,Taylor,11,99
Jason,Cook,12,84
Shirley,Myers,9,68
Christine,Andrews,12,70
```

If you ever need to generate fake data, check out [Mockaroo](https://www.mockaroo.com/). 
