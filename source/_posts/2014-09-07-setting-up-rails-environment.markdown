---
layout: post
title: "Setting up Rails Environment"
date: 2014-09-07 01:23:19 +0900
comments: true
categories: Rails, Ruby, rvm, gemset, gem
description: Setting up Rails Environment
keywords: Rails, Ruby, rvm, gemset, gem
---
Time to install Ruby and Rails...
<!-- more -->
## Installing Ruby

Running OS X or Linux use Ruby Version Manager (rvm) to install and manage different versions of ruby.

####1. Install rvm:
```
$ curl -sSL https://get.rvm.io | bash -s stable
```

####2. Update to the latest version of rvm:
```
$ rvm get stable
```

####3. Check the requirements to install Ruby:
```
$ rvm requirements
```

####4. Using Homebrew on OSX you can install any missing libraries/apts:
```
$ brew install libtool libxslt libksba openssl libyaml
```

On Linus use apt-get or yum:
```
# Debian
$ apt-get install libyaml-dev

# Fedora/RHEL/CentOS
$ yum install libyaml-devel
```

####5. Install Ruby:
```
$ rvm install 2.0.0 --with-openssl-dir=$HOME/.rvm/usr
```

####6. Check ruby version installed:
```
$ rvm list
```

####7. Check version of ruby in use:
```
$ ruby -v
```

## Gemsets
Gems are essentially self contained packages of ruby code.  Due to possible conflict of gem versions it is useful to tie a particular `gem version` used for a particular `ruby version`.  We associate these into a `gemset`.

####1. Create a gemset for a ruby version:
```
rvm use 2.0.0@railstutorial_rails_4_0 --create --default
```

This command creates `(--create)` the gemset `railstutorial_rails_4_0` associated with `Ruby 2.0.0` while arranging to start using it immediately (use) and setting it as the default `(--default)` gemset, so that any time we open a new terminal window the `2.0.0@railstutorial_rails_4_0` Ruby/gemset combination is automatically selected.

RVM gives you a separate gem directory for each and every Ruby version and gemset. This means that gems must be explicitly installed for each revision and gemset.

### Gemset commands

####1. To see the name of the current gemset
```
$ rvm gemset use teddy
$ rvm gemset name
teddy
```

####2. To list the full directory path for the current gemset:
```
$ rvm gemdir
 /Users/rys/.rvm/gems/2.1.1@teddy
```

####3. To list all named gemsets for the current ruby interpreter
```
$ rvm gemset list

 global
 teddy
```

## RubyGem
Package manager for ruby projects and installed as part of rvm.  

####1. To check version:
```
$ which gem
```

####2. Freeze to a gem
Freezing a system to a particular version to prevent conflict should RubyGem change:
```
$ gem update --system 2.1.9
```

####3. Suppress ri and rdoc documentation due to build time. 

Create a `~/.gemrc` file with the following contents:

{% codeblock ~/.gemrc %}
install: --no-rdoc --no-ri
update:  --no-rdoc --no-ri
{% endcodeblock %}

## Install Rails
####1. Instal rails 4.0.8 for example:
```
$ gem install rails --version 4.0.8
```

####2. Check version:
```
$ rails -v
Rails 4.0.8
``` 
