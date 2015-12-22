---
title: Writing to CSVs
layout: post
date: 2015-11-21 23:59:50
permalink: writing-to-csvs
---

In this section, we'll write to a CSV file. 

{% highlight ruby %}
CSV.open('new_people.csv', 'w') do |csv|
  csv << ["first_name", "last_name"]
  csv << ["Rachel", "Warbelow"]
end
{% endhighlight %}

Check out the <a href="http://ruby-doc.org/core-2.0.0/IO.html#method-c-new-label-IO+Open+Mode">I/O Mode Ruby Docs</a> for more info on modes that can be passed in. 

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>Generating honor roll CSV file</span>
    <p>
      Write a program that takes a command line argument of the original csv file and outputs a file `honor-roll.csv` that contains only the names of students who scored 90 or higher from the original file. 
    </p>
  </div>
</div>

`students.csv`

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