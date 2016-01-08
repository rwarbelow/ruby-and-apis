---
title: API Project
layout: post
date: 2015-01-04 23:59:54
permalink: api-project
---

### Nutrition

Use the <a href="http://www.nutritionix.com/business/api">Nutritionix API</a> to create an interface where a user enters the following command:

$ ruby nutrition.rb -f taco

Where -f represents a food to search for. The user should receive a CSV file containing nutrition information about tacos.

### Top News Stories

Use the <a href="http://developer.nytimes.com/docs/top_stories_api/">NYTimes Top Stories API</a> to create an interface where a user enters the following command:

$ ruby top_stories.rb -s sports

Where -s represents the section. The user should receive a CSV file where the title is today's date and "top-stories" -- for example: 2016-1-8-top-stories.csv. The CSV should contain the article titles, authors, date published, abstract, and url to the article.  