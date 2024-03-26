#ruby #module #usage #definition

A module in Ruby is a collection of methods, constants, and class variables. Modules are defined much like classes, but they cannot be instantiated or subclassed and do not have per-instance variables or methods. Modules are excellent for namespacing and for sharing functionality between classes.

## Definition

``` ruby
module MyModule
  # Module content goes here.
end
```

## Usage

``` ruby
$LOAD_PATH << './path/to/module'
require 'my_module'

class MyClass
  include MyModule
  # Class content goes here.
end
```
