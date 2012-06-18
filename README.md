# randumb

[![Build Status](https://secure.travis-ci.org/spilliton/randumb.png?branch=master)](http://travis-ci.org/spilliton/randumb)

randumb is a ruby gem that allows you to easily pull random records via ActiveRecord

Requires ActiveRecord 3.0.0 or greater

## Usage

``` ruby
# returns a single record when called without parameters
Artist.random # returns a random instance of Artist if there are any, otherwise nil

# returns an array if called with an integer param
Artist.random(3)  # returns an array of three Artists picked at random
Artist.random(1)  # returns an array containing one random Artist
```

``` ruby
# randumb works like the active record "all, first, and last" methods
# so you can put it at the end of scopes and relations
Artist.has_views.includes(:albums).where(["created_at > ?", 2.days.ago]).random(10)
# in the prior example, if only 5 records met the where conditions, 
# randumb will return an array with those 5 records in random order
```

As of version 0.2.0, randumb works by tacking on an additional RANDOM() order to the scope.
This means it will have the least amount of sort precedence if you are already including other ordering.

### Stacking the deck

You can use ```random_weighted``` to favor certain instances more than others.

If you want to favor showing higher-rated Movies, for example, and your
Movie model has a numeric ```score``` column, you can use ```Movie.random_weighted_by_score```.

Higher-scored movies will be more likely to be returned than lower-scored movies, in proportion to their ```score```.


## Why

I built this for use on [Compare Vinyl][comparevinyl].  Check out the homepage to see it in action :)

## Install 

``` ruby
# Add the following to you Gemfile
gem 'randumb'
# Update your bundle
bundle install
```

[comparevinyl]: http://www.comparevinyl.com/

## Changelog

### 0.3.0

* Added ```random_weighted```
