#ruby #class #classes #object #attributes #oop #definition #setters #getters

A class in Ruby is a blueprint from which individual objects are created. Class definitions include method definitions, variable definitions, and more.

## Definition

Here's an example of how to define a class in Ruby:
``` ruby
class Student
  # Class content goes here
end
```

## Attributes

Class attributes are variables that belong to an instance of a class. You define class attributes by adding `@` before them:

``` ruby
class Student
  @first_name
  @last_name
  @email
  @username
  @password
end
```

## Setters and Getters

Setters and getters are methods that allow you to set and get the values of class attributes. In Ruby, you can use `attr_accessor` to automatically create setters and getters:

``` ruby
class Student
  attr_accessor :first_name, :last_name, :username, :email, :password
end
```

In this case, `attr_accessor` creates both a setter and a getter for `first_name`, `last_name`, `username`,  `email`, and `password`.

If you want to create a read-only attribute (i.e., an attribute with a getter but no setter), you can use `attr_reader`:

``` ruby
class Student
  attr_reader :username
end
```

In this case, `attr_reader` creates a getter for `username`, but no setter.

## Instance Methods

Instance methods are methods that are available on instances of a class. Here are some instance methods for the `Student` class:

``` ruby
class Student
  def set_username
    @username = "#{@first_name}_#{@last_name}".downcase.gsub(/\s+/, '_')
  end

  def to_s
    "First name: #{@first_name}, Last name: #{@last_name}, Email: #{@email}, Username: #{@username}"
  end
end
```

# Initialize Method

The `initialize` method in Ruby classes is a special method that gets called whenever an object is created using the class. This method is typically used to set up initial state for the object, such as setting initial values for instance variables.

Here's an example of how to use the `initialize` method in the `Student` class:

``` ruby
$LOAD_PATH << '.'
require 'authentication'

class Student
  include Authentication
  attr_accessor :first_name, :last_name, :username, :email, :password

  def initialize(first_name, last_name, email, password)
    @first_name = first_name
    @last_name = last_name
    @email = email
    @username = set_username
    
	# Use the create_hash_digest method from the Authentication module.
    @password = create_hash_digest(password)
  end
  
  def set_username
    @username = "#{@first_name}_#{@last_name}".downcase.gsub(/\s+/, '_')
  end
  
  def to_s
    "First name: #{@first_name}, Last name: #{@last_name}, Email: #{@email}, Username: #{@username}"
  end
end
```

In this case, the `initialize` method takes four parameters (`first_name`, `last_name`, `email`, and `password`) and sets the corresponding instance variables to the values of these parameters.

You can create a new `Student` object with initial values like this:

``` ruby
student = Student.new('John', 'Doe', 'john.doe@example.com', 'johndoe')
```

In this case, `student` is a new `Student` object with `first_name` set to `'Christos'`, `last_name` set to `'Mourtogiannis'`, `email` set to `'c.mourtogiannis@gmail.com'`, and `username` set to `'christos_mourtogiannis'`.