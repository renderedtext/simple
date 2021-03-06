# Simple [![TravisCI][travis-img]][travis-ci] [![Dependency Status][gemnasium-img]][gemnasium]

[travis-img]: https://secure.travis-ci.org/bry4n/simple.png?branch=master
[travis-ci]: http://travis-ci.org/bry4n/simple
[gemnasium-img]: https://gemnasium.com/bry4n/simple.png?travis
[gemnasium]: https://gemnasium.com/bry4n/simple

_Simple web development framework for Ruby._

## Installation

**_Notes: Simple is very new and still under development._** Feel free to create ticket and report about bug or improvement or addition.


put this line in your Gemfile

    gem "simple"

or install with `gem` command line

    gem install bundler

## Features

* Barebone Framework; Simple doesn't ship with dependencies like Tilt, Helpers, etc. You can build your own stack for your application.
* Built on top of [Rack](https://github.com/rack/rack) and [http_router](https://github.com/joshbuddy/http_router)
* Insanely small ruby web framework - < 100 LC
* Blazingly fast [benchmark](https://github.com/bry4n/simple/blob/master/examples/benchmark.log)
* Inspired by [Sinatra](https://github.com/sinatra/sinatra)
* Works with [Thin](http://code.macournoyer.com/thin/), [Unicorn](http://unicorn.bogomips.org/), [Pow](http://pow.cx/), [Heroku](http://www.heroku.com/)
* sinatra-like DSL (get, post, put, and delete)

## Basic Usage

The little snippet of the famous hello world web application.

```ruby
# config.ru

require 'simple'
  	
class Example < Simple::Base

  # GET /
  get "/" do
    [200, {"Content-Type" => "text/plain"}, ["Hello World"]]
  end

  # POST /
  post "/" do
    "Posted!"
  end

  # GET /hello
  get "/:message" do
    "You said: #{params[:message]}"
  end

  # POST /users
  post "/users" do
    render :index
  end

  # GET /api/v1/users
  namespace :api do
    namespace :v1 do
      get "/users" do
        halt "Not found", 404
      end
    end
  end

  # render :index
  def self.render(template)
    # Tilt code here or any template engines
  end

  # halt "Access denied!"
  def self.halt(message, status=403)
   [status, {"Content-Type" => "text/plain"}, [message]
  end

end
  
run Example
````

This would create a Rack application. Run the application with `rackup` or `thin` or `unicorn` command line.

## Contribution

* Fork the project
* Make your feature addition or bug fix.
* Add test for it
* Send me a pull request. Topic branches preferred.

## Copyright

Copyright © 2012 Bryan Goines. See LICENSE for details.
