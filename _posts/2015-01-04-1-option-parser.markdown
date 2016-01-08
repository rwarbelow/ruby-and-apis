---
title: Option Parser
layout: post
date: 2015-01-04 23:59:59
permalink: option-parser
---

Ruby's OptionParser class is an alternative to accessing command line arguments using ARGV. Unlike with ARGV, the order of command line arguments does not matter. Values are tagged using a flag ("-n", "-e", etc.)

There are four steps to making an options parser:

1. Define an empty options hash.
2. Create a new instance of the `OptionParser` class.
3. Create a new option by calling the `on` method on the block parameter: `opts.on()`
4. Call `parse!` on the object to execute. 


{% highlight ruby %}
require 'optparse'

options = {}

parser = OptionParser.new do |opts|
  opts.on('-n', '--name name', 'Name') do |name|
    options[:name] = name;
  end
end

parser.parse!

if options[:name]
puts "Hello, #{options[:name]}."
end
{% endhighlight %}

To run this program from the command line: $ ruby options_parser.rb -n Rachel
<br><br><br>
The OptionParser also allows boolean values. In this case, the block parameter will represent true. 

{% highlight ruby %}
require 'optparse'

options = {}

parser = OptionParser.new do |opts|
  opts.on('-n', '--name name', 'Name') do |name|
    options[:name] = name;
  end

  opts.on('-e', '--enthusiasm', 'Enthusiasm') do |e|
    options[:enthusiasm] = e
  end
end

parser.parse!

if options[:enthusiasm] && options[:name]
  puts "HELLO, #{options[:name].upcase}!"
elsif options[:name]
  puts "Hello, #{options[:name]}."
else
  puts "Enter a name using the --name flag."
end
{% endhighlight %}

<div class="card blue-grey darken-1">
  <div class="card-content white-text">
    <span class="card-title orange-text"><b>Try it: </b>OptionParser with Find and Replace</span>
    <p>
      Revise your `find_and_replace.rb` file to accept options from the command line using OptionParser. The interface should look like this: 
    </p> <br>
    <p>
      {% highlight css %}
      $ ruby find_and_replace.rb -s cheese-ipsum.txt -f brie -r cheddar
      {% endhighlight %}
    </p> <br>
    <p>where -s indicates the source, -f indicates the word to find, and -r indicates the replacement word.</p>
  </div>
</div>
