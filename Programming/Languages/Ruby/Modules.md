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

## `include` vs `extend` vs `prepend`

| Mixin | Adds module methods as | Method resolution order |
| ----- | ----------------------- | ------------------------ |
| `include` | Instance methods on the class | Module is inserted just above the class in the ancestor chain |
| `extend` | Class methods on the class (or singleton methods on an object) | N/A, methods are called directly on the receiver |
| `prepend` | Instance methods on the class | Module is inserted just below the class, its methods run *before* the class's own same-named methods, letting the module call `super` to reach them |

``` ruby
module Greetable
  def greet
    "Hello, #{name}"
  end
end

module Loud
  def greet
    super.upcase # `super` reaches the method `Loud` is prepended in front of.
  end
end

class Person
  extend Greetable   # `Person.greet` (class method).
  prepend Loud        # `person.greet` runs `Loud#greet` first, then `Person#greet` via `super`.
  include Greetable  # `person.greet` (instance method), overridden by `prepend` above.

  attr_reader :name

  def initialize(name)
    @name = name
  end

  def greet
    "Hi, #{name}"
  end
end
```

`prepend` is the tool for wrapping/decorating an existing method (e.g. adding logging around a library method) without editing or monkey-patching the original class body.
