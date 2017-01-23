# Ruby Monk Notes on Ruby Primer - Ascent

> Last Updated on Nov 14th 2015.

## 0.1 Blocks

- Official definition of blocks - "A section of code which is grouped together".
- or "A block is code that you can store in a variable like any other object and run on demand."
- The `lambda` keyword is what is most commonly used to create a block in Ruby.
- So, A block is like a method, but one that isn’t associated with any object.
- `lambda` blocks are objects of `Proc` class.
- `call` method is used to execute a lambda.

Converting an method into a block with `to_proc` method.

<pre><code class="ruby">
class Calculator
  def add(a, b)
    return a + b
  end
end

addition_method = Calculator.new.method("add")
addition =  addition_method.to_proc

puts addition.call(5, 6)
</code></pre>

### `yield`

- without using `yield`

<pre><code class="ruby">
def calculation(a, b, operation)
  operation.call(a, b)
end

puts calculation(5, 6, lambda { |a, b| a + b }) # addition
puts calculation(5, 6, lambda { |a, b| a - b }) # subtraction
</code></pre>

- As you can see, the calculation method accepts two numbers and a block that can perform a mathematical operation.
- with `yield`

<pre><code class="ruby">
def calculation(a, b)
  yield(a, b)
end

puts calculation(5, 6) { |a, b| a + b } # addition
puts calculation(5, 6) { |a, b| a - b } # subtraction
</code></pre>

- How `yield` is different from the first example.
  * The block is now no longer a parameter to the method. The block has been implicitly passed to the method - note how it's outside the parentheses.
  * Yield makes executing the block feel like a method invocation within the method invocation rather than a block that's being explicitly called using Proc#call.
  * You have no handle to the block object anymore - yield "magically" invokes it without any object references being involved.

- Yield is not a method, even though it looks like one.
- Doing a yield when there's no block can have unfortunate consequences - an exception (a LocalJumpError) with the message "no block given" is raised
- To defend against this outcome, Ruby offers the `block_given?` method that tells you if a block has been passed to a method implicitly.

## 0.2 Implicit and Explicit Blocks
- Sometimes, the performance benefits of implicit block invocation are outweighed by the need to have the block accessible as a concrete object.
- Converting from implicit to Explicit.

<pre><code class="ruby">
def calculation(a, b, &block) # &block is an explicit (named) parameter
 block.call(a, b)
end

puts calculation(5, 5) { |a, b| a + b } # this is an implicit block
                                        # -- it is nameless and is not
                                        # passed as an explicit parameter.  
</code></pre>

- Converting from Explicit to Implicit.

<pre><code class="ruby">
def calculation(a, b)
  yield(a, b) # yield calls an implicit (unnamed) block
end

addition = lambda {|x, y| x + y}
puts calculation(5, 5, &addition) # like our last example, &addition is
                                  # an explicit (named) block
                                  # -- but `yield` can still call it!
</code></pre>

- Simple set of syntactic rules to convert blocks from one form to the other:
  * The block should be the last parameter passed to a method.
  * Placing an ampersand (&) before the name of the last variable triggers the conversion.
- The convention is to use curly braces for blocks with just a single line of code, and do-end when more than one line is involved.

## 0.4 Blocks, Procs, and Lambdas

- A block created with `lambda` behaves like a method when you use return and simply exits the block, handing control back to the calling method.
- A block created with `Proc.new` behaves like it’s a part of the calling method when return is used within it, and returns from both the block itself as well as the calling method.
- As a consequence, Proc.new is something that’s hardly ever used to explicitly create blocks because of these surprising return semantics. It is recommended that you avoid using this form unless absolutely necessary.

<pre><code class="ruby">
puts lambda {}
puts Proc.new {}
</code></pre>

- The `->` literal form is a shorter version of Kernel#lambda. The following two lines produce identical results.

<pre><code class="ruby">
short = ->(a, b) { a + b }
puts short.call(2, 3)

long = lambda { |a, b| a + b }
puts long.call(2, 3)
</code></pre>

- `Kernel#proc` factory method is identical to Proc.new. Note that proc is a method and not a literal form like -> nor a keyword like yield.

<pre><code class="ruby">

short = proc { |a, b| a + b }
puts short.call(2, 3)

long = Proc.new { |a, b| a + b }
puts long.call(2, 3)
</code></pre>

## 1.0 Classification

- Ruby gives us a method `is_a` that lets us ask which class does the object belongs to.
- As you've probably guessed, Object.`is_a?` accepts a single parameter - a class. Object#is_a? has an alias, Object#kind_of?.
- When classifying objects, it's fairly common to start out with general classes and then delve in to create sub-classes that are more specialized.
- This kind of parent-child relationship between classes is often referred to as inheritance, where the specialized class inherits the abilities of its more generic parent.
- The `Class#superclass` method tells you which class any given class was inherited from.

<pre><code class="ruby">
puts Float.superclass    # Numeric
puts Numeric.superclass  # Object
puts Object.superclass   # BasicObject
</code></pre>

- All Inheritance Chains in ruby end in `BasicObject`. Calling BasicObject's superclass method returns `nil`.

## 1.2 Inheriting Class

- `<` syntax is used to indicate inheritance of one class to another

<pre><code class="ruby">
class Rectangle
  def initialize(length, breadth)
    @length = length
    @breadth = breadth
  end

  def perimeter
    2 * (@length + @breadth)
  end
end

# Create a class Square here
class Square < Rectangle
  def initialize(side)
    @length = @breadth = side
  end
end
</code></pre>

- Square inherits from the Rectangle class and get perimeter method for free.

## 1.3 Redefining, overriding, and `super`

- __Redefining__ a method involves simply replacing one method with another. The original method is simply... lost.
- Since almost every method in Ruby can be redefined, great care must be taken especially with core Ruby classes like Object, Array and so on. A thoughtless method redefinition can break the language entirely
- __Overriding__ in the context of classes involves defining a method in a subclass that is already defined in the superclass. This results in the method being overridden in the subclass, but doesn't in any way affect the method in the superclass.
- Most object oriented languages offer a mechanism by which an overridden method can be called by the overriding method. Ruby uses the `super` keyword to make this happen.
- A common use of inheritance is to have overridden methods in a subclass do something in addition to what the superclass method did, rather than something entirely different, and thats where `super` keyword comes into play.

## 2.0 Instance Variables and Accessors
- __Instance Variables__ are bound to an instance of a class and together forms what we call the state of an object. Every instance of a class has a different set of instance variables.
- Ruby Rules: if your variable does not start with a `@`, it is considered to be a local variable, and not an __Instance Variable__. A local variable is available only inside the method it is defined. It is not shared across the entire object.
- The instance variable is bound to the specific instance of the class. By binding itself to the entire object, an instance variable makes itself available to every method of the object.

- Only the object's own methods can access its instance variables. So, you can have methods known as __getter__ methods whose sole purpose is to return the value of a particular instance variable.
- Having to explicitly define __getter__ methods ensures that the object is always in control of how your state is exposed to the public.

- To execute the statement item.color = 'red', Ruby invokes the the method Item#color= and passes the value 'red' to it. This means that all __setter__ methods end with the = sign in their names.

- An Example for showing __getters__ and __setters__ in action.
<pre><code class="ruby">
class Item
  def initialize(item_name, quantity)
    @item_name = item_name
    @quantity = quantity
  end

  def quantity=(new_quantity)
    @quantity = new_quantity
  end

  def quantity
    @quantity
  end  
end

item = Item.new("a",1)
item.quantity = 3
p item.quantity
</code></pre>

### attr_accessors
- Ruby provides a couple of methods to make life easy when declaring getters and setters for your object.
- The `attr_reader` method defines the reader method for you. This is a convenient shortcut that you can use when your getter simply returns the value of the variable of the same name.
- The `attr_writer` method defines a setter method that sets the value of the instance variable of the same name as the setter.
- In some cases you might want to expose both the getter and setter for an instance variable. then, you can use another method, the `attr_accessor`, which will define both the getter and setter.

- Ruby restricting access to instance variables except through getters and setters is not a limitation of the language, but a deliberate constraint.

## 2.1 Class Variables and Methods

- Any method definition without the self qualifier is by default an instance method.
- Defining Class Methods example

<pre><code class="ruby">
class Item
  def self.show
    puts "Class method show invoked"
  end  
end

Item.show
</code></pre>

- In `def self.show`, the keyword `self` denotes that the method show is being defined in the context of the Class itself, not its instances.
- There is one more way of declaring class methods.

<pre><code class="ruby">
class Item
  class << self
    def show
      puts "Class method show invoked"
    end
  end

end

Item.show
</code></pre>

- __NOTE__: Class methods do not have access to instance methods or instance variables. However instance methods can access both class methods and class variables.

- __Class variables__ are prefixed with `@@`.
- One of the places where class variables do find proper use is to store application configuration - things like application name, version, database and other settings.

<pre><code class="ruby">
class ApplicationConfiguration
  @@config = Hash.new
  def self.set(property_name, value)
    @@config[property_name] = value
  end

  def self.get(property_name)
    @@config[property_name]
  end  
end

ApplicationConfiguration.set("name", "Demo Application")
ApplicationConfiguration.set("version", "0.1")

p ApplicationConfiguration.get("version")

</code></pre>

- __Class Inheritance Variables__ example.

<pre><code class="ruby">
class ApplicationConfiguration
  @configuration = {}

  def self.set(property, value)
    @configuration[property] = value
  end

  def self.get(property)
    @configuration[property]
  end
end

class ERPApplicationConfiguration < ApplicationConfiguration
  @configuration = {}
end

class WebApplicationConfiguration < ApplicationConfiguration
  @configuration = {}
end

ERPApplicationConfiguration.set("name", "ERP Application")
WebApplicationConfiguration.set("name", "Web Application")

p ERPApplicationConfiguration.get("name")
p WebApplicationConfiguration.get("name")

p ApplicationConfiguration.get("name")
</code></pre>

- Prefer __class instance variables__ over __class variables__ when you do really need store data at a class level. Class instance variables use the same notation as that of an instance variable. But unlike instance variables, you declare them inside the class definition directly.

- It is almost always a bad idea to use a __class variable__ to store state. There are only a very few valid use cases where class variables are the right choice.

- __Instance__ variables are available only for instances of a class. They look like @name. Class variables are available to both class methods and instance methods. They look like @@name


## 2.2 Equality of Objects

- Checking for equality of two objects.

<pre><code class="ruby">
class Item
    def initialize(item_name, qty)
        @item_name = item_name
        @qty = qty
    end
end

p Item.new("abcd",1)  == Item.new("abcd",1) #=> false
</code></pre>

- That is the wrong answer! Both objects have exactly the same state and behaviour (since they belong to the same class) and should have been treated as identical objects.

- In Ruby, all binary operators (those which have two operands) including == are actually methods that gets invoked on the parameter on the left-hand side of the operator.

- Fixing the equality operator example.

<pre><code class="ruby">
class Item
    attr_reader :item_name, :qty

    def initialize(item_name, qty)
        @item_name = item_name
        @qty = qty
    end
    def to_s
        "Item (#{@item_name}, #{@qty})"
    end
    def ==(other_item)
      @item_name == other_item.item_name && @qty == other_item.qty
    end
end

p Item.new("abcd",1)  == Item.new("abcd",1)
p Item.new("abcd",2)  == Item.new("abcd",1)
</code></pre>

- Even though overriding `==` worked for simple equality comparisons, there are some cases where that isn't just enough. There are a lot of operations in Ruby that need to check the equality of two objects. While `==` serves the purpose well, it is not really fast.

- Ruby provides a `hash` method with every object. It returns a numeric value which is usually unique to every object.
- So instead of comparing two objects using `==`, which could be expensive when the objects are large, Ruby uses the `hash` of the object when possible.

- The hash method returns the result of XORing all the instance variables that determine the state of the object
