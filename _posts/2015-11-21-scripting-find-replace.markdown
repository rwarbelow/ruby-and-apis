---
title: Scripting Find and Replace
layout: post
date: 2015-11-21 23:59:52
---

In this section, we'll learn about two string methods `#sub` and `#gsub`, figure out how to take in command-line arguments to use in a Ruby program, and create regex patterns to find parts of strings. We'll use these tools to create a command-line program that can read in a file, find and replace content, and write the output back into that file.  

#### String method `#sub`

* [gsub](http://ruby-doc.org/core-2.2.4/String.html#method-i-gsub)

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title">Challenge #1</span>
    <p>
      I am a very simple card. I am good at containing small bits of information.
    </p>
  </div>
  <div class="card-content card-action orange-text">
    <span class="activator orange-text">answer</span>
  </div>
  <div class="card-reveal">
    <span class="card-title orange-text">close</span>
    <p>Here is some more information about this product that is only revealed once clicked on.</p>
    {% highlight ruby %}
    def foo
      puts 'foo'
    end
    {% endhighlight %}
  </div>
</div>

#### String method `#gsub`

* [gsub](http://ruby-doc.org/core-2.2.4/String.html#method-i-gsub)

#### Taking in command line arguments with `ARGV`

* ARGV
* regex
* [rubular](http://rubular.com/)
