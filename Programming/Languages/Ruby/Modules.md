#ruby #module #usage #definition

A module in Ruby is a collection of methods, constants, and class variables. Modules are defined much like classes, but they cannot be instantiated or subclassed and do not have per-instance variables or methods. Modules are excellent for namespacing and for sharing functionality between classes.

## Definition

``` ruby
module MyModule
  # Module content goes here.
  # Do not add self. before the methods if you want to use them via include.
end
```

## Usage

More details about the `LOAD_PATH` and `require` functionality can be found at the [[Dependencies]] notes.

``` ruby
$LOAD_PATH << './path/to/module'
require 'my_module'

class MyClass
  include MyModule
  # Class content goes here.
end
```
