#ruby #class #classes #object #attributes #oop #definition #setters #getters

A class in Ruby is a blueprint from which individual objects are created.

## Definition

``` ruby
class Student
end
```

## Instance Variables and Attributes

Instance variables (`@name`) hold per-object state. They aren't declared ahead of time, they come into existence the first time they're assigned, typically inside `initialize`.

`attr_accessor` generates a getter and setter, `attr_reader` only a getter, `attr_writer` only a setter:

``` ruby
class Student
  attr_accessor :first_name, :last_name, :email
  attr_reader :username # Read-only, no attr_accessor for this one.
end
```

## Initialize and Instance Methods

`initialize` runs when `Student.new(...)` is called, and is where instance variables normally get their first value:

``` ruby
class Student
  attr_reader :first_name, :last_name, :username

  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
    @username = "#{first_name}_#{last_name}".downcase.gsub(/\s+/, '_')
  end

  def to_s
    "#{first_name} #{last_name} (#{username})"
  end
end

student = Student.new('John', 'Doe')
student.username # => "john_doe"
```

## Class-Level Methods

`class << self` reopens the class itself and defines methods directly on it, useful for grouping several class-level methods together instead of prefixing each with `def self.`:

``` ruby
class Student
  class << self
    def find_by_username(username)
      all.find { |student| student.username == username }
    end

    def all
      @all ||= []
    end
  end
end
```

## Memoization

`@ivar ||= ...` caches the result of an expensive computation on first access. See [[Best Practices]] for the `defined?` guard needed when the cached value can be `nil`/`false`.

## Equality

By default, `==` compares object identity. Override it (and `eql?`/`hash` if the object is used as a `Hash` key or in a `Set`) to compare by value instead:

``` ruby
class Student
  def ==(other)
    other.is_a?(Student) && username == other.username
  end
  alias eql? ==

  def hash
    username.hash
  end
end
```

## Freezing

`freeze` makes an object immutable, any attempt to mutate it afterward raises `FrozenError`. Useful for value objects and constants:

``` ruby
STUDENT_STATUSES = %w[active inactive graduated].freeze
```
