#dependencies #require #include #load-path #gems #libraries

## Gems

Ruby gems are packages of Ruby code that add functionality to your Ruby applications. You can install gems using the `gem install` command in your terminal.

For example, to install the `bcrypt` gem, you would run:

``` shell
gem install bcrypt
```

You can also specify a version of the gem to install:

``` shell
gem install bcrypt -v 3.1.7
```

## Require

In Ruby, `require` is a method that is used to load another file and execute all its statements. This is typically used to load Ruby libraries or modules.

Here's an example:

``` ruby
require 'bcrypt'
```

In this case, the `bcrypt` library is loaded, providing a simple way to securely hash passwords.
You can then iterate through different paths of the module using the `::` and access different functions of it using the `.`. For instance the `BCrypt::Password.create` function is a specific method provided by the `bcrypt` gem, to create a hashed password.

## $LOAD_PATH

`$LOAD_PATH` is a global array in Ruby that contains the list of directories to be searched when loading files with `require`.

If you want to add a directory to this array, you can use the `<<` operator:

``` ruby
$LOAD_PATH << '/path/to/my/directory'
```

Now, Ruby will also look in `/path/to/my/directory` when you use `require`.

For example, if you have a directory structure like this:

``` txt
/my_project
  /lib
    my_module.rb
  main.rb
```

And you want to use `my_module.rb` in `main.rb`, you could modify `$LOAD_PATH` in `main.rb` like this:

``` ruby
$LOAD_PATH << './lib'
require 'my_module'
```

Now, Ruby will look in the `./lib` directory when you use `require 'my_module'`, and `my_module.rb` will be loaded.

## Include

`include` is a method used in Ruby to mix in module methods into a class. When a class includes a module, it gains access to all of its methods.

Here's an example:
``` ruby
module MyModule
  def hello
    'Hello, world!'
  end
end

class MyClass
  include MyModule
end

obj = MyClass.new
puts obj.hello  # Outputs: Hello, world!
```

In this case, `MyClass` includes `MyModule`, so instances of `MyClass` can use the `hello` method.