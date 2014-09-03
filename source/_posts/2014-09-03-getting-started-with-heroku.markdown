---
layout: post
title: "Getting Started with Heroku"
date: 2014-09-03 19:29:22 +0900
comments: true
categories: [Heroku, domain registration] 
---
Quick and dirty guide to get you hosting your site online with Heroku.  I pulled most of the details from [heroku dev site](https://devcenter.heroku.com/articles/getting-started-with-ruby#introduction "Heroku setup").

### 1.  Sign up for Heroku and Install the Toolbelt

[It it here](https://devcenter.heroku.com/articles/getting-started-with-ruby#set-up "Heroku Toolbelt").


### 2.  Log into heroku from console:
        $ heroku login 


### 3. Head into project:
        $ git clone https://github.com/heroku/ruby-getting-started.git
        $ cd ruby-getting-started

### 4. Create heroku remote repo and generate app name:
        $ heroku create
        Creating polar-inlet-4930... done, stack is cedar
        http://polar-inlet-4930.herokuapp.com/ | git@heroku.com:polar-inlet-4930.git
        Git remote heroku added

This also creates a remote repository (called _heroku_) which it configures in your local git repo. Heroku generates a random name (in this case _polar-inlet-4930_) for your app - you can pass a parameter to specify your own, or rename it later with `$ heroku rename <<my_name>>` 

Just remember to check the `.git/config` that the remote url is now pointing to the correct heroku git repository. Otherwise run this: `$ git remote set-url heroku git@heroku.com:<app_name>.git`

### 5. Deploy it:
        $ git push heroku master

### 6. Enable a instance to be running:
        $ heroku ps:scale web=1

### 7. Open website.
        $ heroku open

Heroku starts up apps by running the `./Procfile`.  Contains something like: 
`web: bundle exec unicorn -p $PORT -c ./config/unicorn.rb`

### 8. Configure to your own domain
If you need to register a new domain name you can get one at [namecheap](https://www.namecheap.com/ "namecheap").

If you are using namecheap you will need to head to `Manage Domains > Modify Domain` and click onto the `All Host Records`. Edit with the Heroku URL e.g. `polar-inlet-4930.herokuapp.com`

        Host Name: www
        IP Address/URL: polar-inlet-4930.herokuapp.com
        Record Type: CNAME (Alias)

Head to Heroku Dashboard, select the appropriate app and add the new domain name.