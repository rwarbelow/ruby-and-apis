---
title: Deploying to Heroku
layout: post
date: 2015-01-04 23:59:49
permalink: deploying-to-heroku
---

Before we get too much further, let's make sure our app runs on production using Heroku. 

<a href="https://www.heroku.com/about">Heroku</a> is a cloud-based platform for easily deploying apps live. Heroku works with git, so the first thing we'll do is remove the existing git reference to my repository:

```
$ rm -rf .git
```

Then re-initialize the repository:

```
$ git init
```

And add and commit:


```
$ git add .
$ git commit -m 'initial commit'
```

Next, sign up for a <a href="https://signup.heroku.com">Heroku account</a>. 

Let's install the Heroku toolbelt by following <a href="https://toolbelt.heroku.com/">these instructions</a>. 

Once we have the toolbelt, we'll create a new Heroku remote:

```
$ heroku create
Creating app... done, stack is cedar-14
https://limitless-thicket-60175.herokuapp.com/ | https://git.heroku.com/limitless-thicket-60175.git
```

Heroku will give you back the URL where your app lives. By default, this is adjective-noun-number.herokuapp.com. You can customize it in your Heroku dashboard if you'd like. 

We can check that this remote was created by asking git:

```
$ git remote -v
heroku  https://git.heroku.com/limitless-thicket-60175.git (fetch)
heroku  https://git.heroku.com/limitless-thicket-60175.git (push)
```

Great! Now we can push to Heroku: 

```
$ git push heroku master
Counting objects: 25, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (20/20), done.
Writing objects: 100% (25/25), 3.90 KiB | 0 bytes/s, done.
Total 25 (delta 0), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> Ruby app detected
remote: -----> Compiling Ruby/Rack
...
```

Next, we'll migrate the database on our Heroku remote:

```
$ heroku run rake db:migrate
Running rake db:migrate on limitless-thicket-60175... up, run.8034
== 20160219213811 CreatePeople: migrating =====================================
-- create_table(:people)
DEPRECATION WARNING: `#timestamps` was called without specifying an option for `null`. In Rails 5, this behavior will change to `null: false`. You should manually specify `null: true` to prevent the behavior of your existing migrations from changing. (called from block in change at /app/db/migrate/20160219213811_create_people.rb:7)
   -> 0.0087s
== 20160219213811 CreatePeople: migrated (0.0088s) ============================
```

You can either navigate to the URL where your app lives via your browser, or type `heroku open`. 

Make sure to check `/people`. You should see a heading *All People*, but since this is running with our production database, we won't actually see any people there. 

