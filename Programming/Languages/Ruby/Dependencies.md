#dependencies #require #include #load-path #gems #libraries

## Gems

Ruby gems are packages published to [rubygems.org](https://rubygems.org/). Install with `gem install <name>`, optionally pinning a version:

``` shell
gem install bcrypt -v 3.1.7
```

## Require and `$LOAD_PATH`

`require` loads a file once and executes it, used to pull in gems or local files. `$LOAD_PATH` is the array of directories Ruby searches to resolve a `require`:

``` ruby
$LOAD_PATH << './lib'
require 'my_module'
```

Namespaced constants inside a loaded file are reached with `::`, e.g. `BCrypt::Password.create` is the `create` method on the `Password` class nested in the `BCrypt` module.

## Include

`include` mixes a module's methods into a class as instance methods:

``` ruby
module Greetable
  def hello
    'Hello, world!'
  end
end

class MyClass
  include Greetable
end

MyClass.new.hello # => "Hello, world!"
```

See [[Modules]] for `extend` and `prepend`, the other two ways to mix in a module.

## Bundler

[Bundler](https://bundler.io/) manages a project's gem dependencies declared in a `Gemfile`, resolving exact versions into `Gemfile.lock` so every environment installs the same set of gems.

``` ruby
# Gemfile
source 'https://rubygems.org'

gem 'bcrypt', '~> 3.1.7'

group :development, :test do
  gem 'rspec'
  gem 'factory_bot'
end
```

`bundle install` installs the gems from the `Gemfile` and writes/updates `Gemfile.lock`, commit the lockfile so installs are reproducible. Run scripts and commands through Bundler's resolved gem set with `bundle exec`, e.g. `bundle exec rspec`, so the loaded gem versions match what's in `Gemfile.lock` rather than whatever happens to be installed system-wide.
