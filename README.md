# sinatra-hello-world

A simple “Hello world!” [Sinatra](http://sinatrarb.com) app that works with [`rbenv`](https://github.com/rbenv/rbenv).

## Create from scratch:

```sh
# create the Sinatra source
echo "require 'sinatra'
get '/' do
  'Hello world!'
end" > api.rb

# declare dependencies  
echo "source 'https://rubygems.org'
gem 'sinatra'
gem 'unicorn'
gem 'json'" > Gemfile   
  
# install and package dependencies
rbenv exec bundle config --local path vendor/bundle
rbenv exec bundle
rbenv exec bundle package
echo "vendor/bundle/**/*" > .gitignore # ignore the bundle sources but save the packaged caches

# create a Procfile and config.ru for Heroku
echo "web: bundle exec unicorn --port \$PORT
local: rbenv exec bundle exec unicorn --port \$PORT" > Procfile

echo "require './api'
run Sinatra::Application" > config.ru
```

> Created with the help of the [Sinatra getting started guide](http://sinatrarb.com/intro.html) and  [Heroku Sinatra-iOS guide](https://devcenter.heroku.com/articles/getting-started-ios-development-sinatra-cedar), captured in PDFs in `docs/`.

# Deployment

## Local

```sh
rbenv exec bundle exec ruby api.rb &
open http://localhost:4567
```

### Locally with Heroku

```sh
heroku local local &
open http://0.0.0.0:5000
```

## Heroku

