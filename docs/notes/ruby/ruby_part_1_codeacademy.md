# Introductory Ruby Notes(P1)
> Based of CodeAcademy Ruby Course. Last Updated 31st Oct 2015.

### Loops
- __The 'Until' Loop__ - Complement to the while loop.

<pre><code class="ruby">
counter = 1
until counter > 10
  puts counter
  counter += 1

end
</code></pre>

- __Inclusive__ vs __Exclusive Ranges__ in Ruby:
    * `..` mean __Inclusive__ range since it includes the final number.
    * `...` mean __Exclusive__ range since it excludes the end number.

-  The Loop Method
    * An __iterator__ is just a Ruby method that repeatedly invokes a block of code.
    * The simplest iterator is the `loop` method.

<pre><code class="ruby">
i = 20
loop do
  i -= 1
  print "#{i}"
  break if i <= 0
end
</code></pre>

- The `next` Keyword: The `next` keyword can be used to skip over certain steps in the loop.

<pre><code class="ruby">
i = 20
loop do
  i -= 1
  next if i%2== 1 # skips when i is odd.
  print "#{i}"
  break if i <= 0
end
</code></pre>

### Hashes
- using the `sort_by`:

<pre><code class="ruby">
colors = {"blue" => 3, "green" => 1, "red" => 2}
colors = colors.sort_by do |color, count|
  count # sort by count
end
</code></pre>

##### Blocks as parameter to a method:
- Passing a block to a method is a great way of __abstracting__ certain tasks from the method and defining those tasks when we call the method.

##### combined comparison operator `<=>`
- used to compare two Ruby objects.
- It returns 0 if the first operand (item to be compared) equals the second, 1 if first operand is greater than the second, and -1 if the first operand is less than the second.
- A block that is passed into the Array.`sort` method must return either 1, 0, -1

##### Nil.
- When we try to access the key that doesn't exist in hash, we get __nil__ and no error is thrown.(Unlike Python's KeyError).
- Along with `false`, `nil` is one of two non-true values in Ruby.


### Symbols in Ruby.
- [x] READ [Understanding Symbols In Ruby | Stack Overflow](http://stackoverflow.com/questions/2341837/understanding-symbols-in-ruby)
- Symbols are Strings, just with an important difference, Symbols are __immutable__.
- Unlike strings, symbols of the same name are initialized and exist in memory only once during a session of ruby. This save some memory
- String are mutable in Ruby. (Unlike python. In a way Ruby Symbols are like python strings.)
- Symbols always start with a colon `:`. hey must be valid Ruby variable names, so the first character after the colon has to be a letter or underscore ; after that, any combination of letters, numbers, and underscores is allowed.
- Symbol-as-keys are faster than strings-as-keys because of the immutability and singleton nature.
- Symbol.`to_s` converts a symbol to as string.
- String.`to_sym` & String.`intern` converts a string into a symbol.
- From Ruby 1.9+, we can use this type of Hash in Ruby as shown below.

<pre><code class="ruby">
new_hash = { one: 1,
  two: 2,
  three: 3
}
</code></pre>

- In this, you put colon `:` at the end of the symbol and you don't need hash-rocket now.

#### Filtering a hash
- Hash.`select` can be used to filter a hash for values that meet certain criteria.

<pre><code class="ruby">
grades = { alice: 100,
  bob: 92,
  chris: 95,
  dave: 97
}

grades.select {|name, grade| grade < 97}
# ==> {:bob=>92, :chris=>95}

grades.select { |k, v| k == :alice }
# ==> {:alice=>100}
</code></pre>

- Hash.`each_key` iterates over all keys and Hash.`each_value` iterates over all values.

<pre><code class="ruby">
my_hash = { one: 1, two: 2, three: 3 }

my_hash.each_key { |k| print k, " " }
# ==> one two three

my_hash.each_value { |v| print v, " " }
# ==> 1 2 3
</code></pre>

### Ruby `case` statements.
- Ruby provides a concise `case` statement when we need to have multiple conditions

<pre><code class="ruby">
case language
when "JS"
  puts "Websites!"
when "Python"
  puts "Science!"
when "Ruby"
  puts "Web apps!"
else
  puts "I don't know!"
end
</code></pre>

- `case` statements can be made more concise and readable like following.

<pre><code class="ruby">
case language
  when "JS" then puts "Websites!"
  when "Python" then puts "Science!"
  when "Ruby" then puts "Web apps!"
  else puts "I don't know!"
end
</code></pre>

#### Conditional assignment operator `||=`
- Assigns a variable if it hasn't already been asssigned.

#### Default Return value from a ruby method
- Ruby's methods will return the result of the last evaluated expression.

#### Ruby's short circuit Evaluation.
- Ruby doesn't look at both expressions unless it has to; if it see `false && true` it stops reading as soon as it sees && because it knows `false &&` anything must be `false`.

<pre><code class="ruby">
def a
  puts "A was evaluated!"
  return true
end

def b
  puts "B was also evaluated!"
  return true
end

puts a || b ## only a is evaluated and only "A was evaluated!" is printed.
puts "------"
puts a && b  ## both a and b are evaluated.
</code></pre>

#### `.upto` and `.downto`
- If we know the range of numbers we'd like to include, we can use `.upto` and `.downto`. This is a much more Rubyist solution than trying to use a `for` loop that stops when a counter variable hits a certain value.

<pre><code class="ruby">
95.upto(100) { |num| print num, " " }
# Prints 95 96 97 98 99 100


"L".upto("P") { |l| print l + " " }
# Print L M N O P and works correctly with numbers.
</code></pre>

### Call and Response
- Ruby is less concerned about what kind of thing an object is and only really cares about what method calls it responds to.
- `.respond_to?` takes a symbol and returns true if an object can receive that method and false otherwise.

<pre><code class="ruby">
[1, 2, 3].respond_to?(:push)   # true
[1, 2, 3].respond_to?(:to_sym) # false
22.respond_to?(:next)          # true
</code></pre>

#### concatenation operator `<<` aka "The shovel"
- Works like Array.`push`

<pre><code class="ruby">
[1, 2, 3] << 4
# ==> [1, 2, 3, 4]

"Yukihiro " << "Matsumoto"
# ==> "Yukihiro Matsumoto" Works on Strings too.
</code></pre>

#### string interpolation with `#{}`
- used for interpolating a variable inside a string.

<pre><code class="ruby">
drink = "espresso"
age = 26

"I love #{drink}."
# ==> I love espresso.
"I am #{age} years old."
# ==> I am 26 years old.
</code></pre>

> Refactoring is just a fancy way of saying we're improving the structure or appearance of our code without changing what it actually does.

#### Array.`collect`
- The `collect` method takes a block and applies the expression in the block to every element in an array.
- `.collect` returns a copy of resultant array, but doesn't change (or mutate) the original array. use `collect!` to mutate the original array.

<pre><code class="ruby">
my_nums = [1, 2, 3]
my_nums.collect { |num| num ** 2 }
# ==> [1, 4, 9]
</code></pre>


### Learning `yield`

__Why do some methods accept a block and others don't?__
- It's because methods that accept blocks have a way of transferring control from the calling method to the block and back again.
- Here we use `yield` to transfer control to the block and back again.

<pre><code class="ruby">
def block_test
  puts "We're in the method!"
  puts "Yielding to the block..."
  yield
  puts "We're back in the method!"
end

block_test { puts ">>> We're in the block!" }

####################### Output ###################
# We're in the method!
# Yielding to the block...
# >>> We're in the block!
# We're back in the method!
# nil
</code></pre>

- we can also pass parameters to `yield`.

<pre><code class="ruby">
def yield_name(name)
  puts "In the method! Let's yield."
  yield("Kim")
  puts "In between the yields!"
  yield(name)
  puts "Block complete! Back in the method."
end

yield_name("Eric") { |n| puts "My name is #{n}." }

####################### Output ###################
# In the method! Let's yield.
# My name is Kim.
# In between the yields!
# My name is Eric.
# Block complete! Back in the method.
</code></pre>

#### Procs in Ruby
- Procs, unlike Blocks, can be saved to variables and have powers & abilities of a real object.
- Think of a proc as a "saved" block. Just like you can give a bit of code a name and turn it into a method, you can name a block and turn it into a proc.
- Procs are easy to define! You just call `Proc.new` and pass in the block you want to save.

<pre><code class="ruby">
cube = Proc.new { |x| x ** 3 }
</code></pre>

- We can then pass the proc to a method that would otherwise take a block, and we don't have to rewrite the block over and over!

<pre><code class="ruby">
[1, 2, 3].collect!(&cube)
# ==> [1, 8, 27]
[4, 5, 6].map!(&cube)
# ==> [64, 125, 216]
</code></pre>

- The `&` is used to convert the cube proc into a block.

__Why bother saving our blocks as procs? There are two main advantages:__

1. Procs are full-fledged objects, so they have all the powers and abilities of objects. (Blocks do not.)
2. Unlike blocks, procs can be called over and over without rewriting them. This prevents you from having to retype the contents of your block every time you need to execute a particular bit of code. (__DRY Principle__)

- Procs, unlike blocks can also be executed by calling `call` on them.
- symbols can be converted into Procs by `&`.

<pre><code class="ruby">
strings = ["1", "2", "3"]
nums = strings.map(&:to_i)
# ==> [1, 2, 3]
</code></pre>

- In above example, By mapping &:to_i over every element of strings, we turned each string into an integer.

### Lambdas in Ruby.
- Like procs, __lambdas__ are objects. They are pretty similar to procs, with litte difference in syntax, and few quirks.
- __lambda syntax__ : `lambda { |param| block }`
- Just like with procs, we'll need to put `&` at the beginning of our lambda name when we pass it to the method.
- Example

<pre><code class="ruby">
strings = ["leonardo", "donatello", "raphael", "michaelangelo"]
symbolize = lambda { |string| string.to_sym } # the lambda
symbols = strings.collect(&symbolize)

# [:leonardo, :donatello, :raphael, :michaelangelo]
</code></pre>

__Lambdas vs Procs__

1. A __lambda__ checks the number of arguments passed to it, while a __proc__ does not. so a __lambda__ will throw an error if you pass wrong number of arguments.
2. When a __lambda__ returns, it passes control back to the calling method; when a __proc__ returns, it does so immediately, without going back to the calling method.

<pre><code class="ruby">
def batman_ironman_proc
  victor = Proc.new { return "Batman will win!" }
  victor.call
  "Iron Man will win!"
end

puts batman_ironman_proc # "Batman will win!" cause proc don't return control to the calling method.

def batman_ironman_lambda
  victor = lambda { return "Batman will win!" }
  victor.call
  "Iron Man will win!"
end

puts batman_ironman_lambda # "Iron Man will win!" cause lambdas return control to the calling method.
</code></pre>

## Review of Blocks, Procs and Lambdas in Ruby.
1. A __block__ is just a bit of code between `do..end` or `{}`. It's not an object on its own, but it can be passed to methods like `.each` or `.select`.
2. A __proc__ is a saved block we can use over and over.
3. A __lambda__ is just like a proc, only it cares about the number of arguments it gets and it returns to its calling method rather than returning immediately.


### Notes on classes.
- You can think of `initialize` as the function that "boots up" each object the class creates. It creates an objects and sets some instance attributes.
- In Ruby, we use `@` before a variable to signify that it's an instance variable. This means that the variable is attached to the instance of the class.
- __class methods__: A class method belongs to the class itself, and for that reason it's prefixed with the class name. Most of the methods we have seen were actually instance methods. Example of how to create __class methods__.

<pre><code class="ruby">

class Machine
  def Machine.hello # This is a class Method,since class name is prefixed.
    puts "Hello from the machine!"
  end
end

</code></pre>

## Scope & classes
- The __scope__ of a variable is the context in which it's visible to the program.

__Four Types of Scoped variables in Ruby__

1. __global variables__: variables that are available everywhere. There are two ways to define them. First, just define the variable outside of any method or class. Second, If you want to make a variable global from inside a method or class, just start it with a `$`. __NOTE__: __global variables__ can be changed from anywhere in your program, and they are generally not a very good idea.
2. __local variables__: ones that are only in available certain methods.
3. __class variables__: variables that are members of a certain class. They are like instance varibles, but instead they belong to a class itself, and not its instances. __class variables__ always start with `@@`.
4. __instance variables__: variables that are only available to particular instances of a class(object). __instance variables__ belong to an instance of the class. and they always start with `@`[single @].

## Inheritance in Ruby
- __Inheritance__ is the process by which one class takes on the attributes and methods of another, and it's used to express an __is-a relationship__. for example.

<pre><code class="ruby">
class ApplicationError
  def display_error
    puts "Error! Error!"
  end
end

class SuperBadError < ApplicationError # This is how to indicate Inheritance.
end

err = SuperBadError.new
err.display_error # It would still work since SuperBadError inherits from ApplicationError.
</code></pre>

- __Inheritance syntax__: `class DerivedClass < BaseClass`. `<` reads like 'inherits from'
- `super` keyword: When you call `super` from inside a method, that tells Ruby to look in the superclass of the current class and find a method with the same name as the one from which `super` is called. If it finds it, Ruby will use the superclass' version of the method.
- Ruby disallows __multiple inheritance__. That means, Any given Ruby class can have only one superclass.
- However, there are instances where you want to incorporate data or behavior from several classes into a single class, and Ruby allows this through the use of __mixins__.


#### Semicolon `;` in ruby
- If you want to end a Ruby statement without going to a new line, you can just type a semicolon.

<pre><code class="ruby">
class Monkey
end

# The above class definition is equivalent to
class Monkey; end
</code></pre>
- This is a time saver when you're writing something very short, like an empty class or method definition.

### `public` and `private` methods in Ruby
- Ruby allows you to explicitly make some methods `public` and others `private`.
- __Public__ methods allow for an interface with the rest of the program.
- __Private__ methods, on the other hand, are for your classes to do their own work undisturbed. Another way to say this is that the method cannot be called with an explicit receiver.
- Methods are __public by default__ in Ruby.
- In order to access private information, we have to create public methods that know how to get it. This separates the _private implementation from the public interface_.

#### `attr_reader`, `attr_writer` and `attr_accessor` in classes
- Ruby needs methods in order to access attributes. That means we need to create getters and setters. Instead, We can use __attr_reader__ to access a variable and __attr_writer__ to change it. for Example.

<pre><code class="ruby">
class Person
  attr_reader :name            # to read the name variable
  attr_writer :name            # to write/modify the name variable.
  def initialize(name)
    @name = name
  end
end
</code></pre>

- We can use __attr_accessor__ to make a variable readable and writeable in one fell swoop.

### Modules
- You can think of a __module__ as a toolbox that contains a set methods and constants.
- __Modules__ are like classes, but they can't create Instances and have subclasses.
- Storing helpful constants in a Module is a great Idea,storing variables not so much. Ruby constants are written in ALL_CAPS and are separated with underscores if there's more than one word.
- One of the main purposes of modules is to separate methods and constants into named spaces. These are called __name-spaces__. This is how ruby doesn't confuse between `Math::PI` and `Circle::PI`.
- `::` is called __scope resolution operator__. It tells Ruby where you're looking for a specific bit of code.
- `require` keyword imports a module into the interpreter.
- with `include`, any class can include a module into itself, and use the module's methods. Also, Since everything has been pulled in, you can simply write `PI` instead of `Math::PI`.
- When a module is used to mix additional behavior and information into a class, it's called a __mixin__. for Eg.

<pre><code class="ruby">
module Action
  def jump
    @distance = rand(4) + 2
    puts "I jumped forward #{@distance} feet!"
  end
end

class Rabbit
  include Action        # including the module Action, therefore creating a mixin here.
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

class Cricket
  include Action       # including the module Action, therefore creating a mixin here.
  attr_reader :name
  def initialize(name)
    @name = name
  end
end

peter = Rabbit.new("Peter")
jiminy = Cricket.new("Jiminy")

peter.jump
jiminy.jump
</code></pre>


- Whereas `include` mixes a module's methods in at the instance level, the `extend` keyword mixes a module's methods at the class level.

<pre><code class="ruby">
# ThePresent has a .now method that we'll extend to TheHereAnd

module ThePresent
  def now
    puts "It's #{Time.new.hour > 12 ? Time.new.hour - 12 : Time.new.hour}:#{Time.new.min} #{Time.new.hour > 12 ? 'PM' : 'AM'} (GMT)."
  end
end

class TheHereAnd
  extend ThePresent
end

TheHereAnd.now
</code></pre>

- NOTE: Ruby also allows underscores in number, to make reading them easier. like 1 million could be written as 1_000_000.
