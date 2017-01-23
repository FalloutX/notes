# Introductory Ruby Notes(P3) - From Ruby Monk

> Last Updated Nov 7th 2015.

### 0.1 More Objects and Methods

- Object.`methods` gives us an array of all the methods available on a given object.
- Array.`sort` sorts a given array.
- Array.`index(element)` gives the index of element in Array.
- Number.`between?(sm, lg)` returns true if Number is between sm and lg numbers.


### 1.0 Introduction to Strings
- 'September' and "September" are called literal strings.
- Any valid block of Ruby code you place inside #{} will be evaluated and inserted at that location.
- A String literal created with single quotes does not support interpolation.
- Double quotes allow for escape sequences while single quotes do not.
- String.`include? "other_string"'` returns true if String contains other_string
- String.`start_with? "prefix"` returns true if String starts with prefix
- String.`end_with? "suffix"` returns true if String ends with suffix.
- It is conventional in Ruby to have '?' at the end of the method if that method returns only boolean values.
- String.`index "substring"` returns the index of first occurence of "substring" in String.
- String.`downcase` returns the lowercase version of String.
- String.`upcase` returns the uppercase version of String.
- String.`swapcase` returns the String with case swapped.


### 1.2 Advanced String Operations
- String.`split(pattern)` splits the String depending on the pattern.
- concatenating string with `+`, `<<` and `String.concat`.
  * 'Ruby' + 'Monk' # returns 'RubyMonk'
  * 'Ruby'.concat('Monk') # returns 'RubyMonk'
  * 'Ruby' << 'Monk' # appends 'Monk' to 'Ruby', giving 'RubyMonk'
  * '<<' is just like '+', but in this case the String object 'Monk' will be appended to the object represented by 'Ruby' itself
- String.`sub(pattern, replacement)` replaces first appearance of pattern with replacement.
- String.`gsub(pattern, replacement)` replaces all occurrences of pattern.
- In Ruby you specify a RegEx by putting it between a pair of forward slashes (/).
- String.`match`converts a pattern to a RegEx, and then invokes its match method on the target String object.


### 2.0 Boolean Expressions in Ruby
- Equality comparison, `==`
- others are `<=`, `>=`, '<', `>`, `!=` with their usual meaning.
- `&&` stands for boolean 'and' and `||` stands for boolean 'or'.
- `!` stands for negation.

### 2.1 The if..else construct
- Ruby gives you the `elsif` keyword that helps you check for multiple possibilities inside an if..else construct, as shown in the example below.

<pre><code class="ruby">
def check_sign(number)
  if number > 0
    "#{number} is positive"
  elsif number == 0
    "#{number} is zero"
  else
    "#{number} is negative"
  end        
end
</code></pre>

- `unless` keyword can used in places where you want to check for a negative condition. for ex.

<pre><code class="ruby">
age = 10
unless age >= 18
  puts "Sorry, you need to be at least eighteen to drive a car. Grow up fast!"
end
</code></pre>

- Ternary operator consists of `?` and `:`,  `?` and `:` can be used to mean "then" and "else" respectively. ex

<pre><code class="ruby">
def check_sign(number)
  number > 0 ? "#{number} is positive" : "#{number} is negative"
end
</code></pre>

- the objects `false` and `nil` equates to `false`, and therefore called __falsy__.  Every other object like say `1`, `0`, `""` are all evaluated to be true, and are called __truthy__.

### 2.2 Loops in Ruby
- `do` loops. Below is an infinite do loop. It doesn't have a termination condition, therefore it never terminates.
<pre><code class="ruby">
loop do
  puts "this line will be executed for an infinite amount of time"
end
</code></pre>
- `break` is used to break out of loops.
- Number.'times' runs a block of code Number times. ex.

<pre><code class="ruby">
5.times do
  # do the stuff that needs to be done
  # This loop is run 5 times.
end
</code></pre>

### 3.0 Introduction to Arrays
- creating an array: `[]` or `Array.new` or `[1,2, other_elements]`
- `array[n]` returns the element at nth index.
- Array indexes can also start from the end of the array, starting from `-1`. this is called __reverse index lookup__.
- `<<` can be used to append elements to the Array. Also Array.`push(el)` does the same thing.

### 3.1 Basic Array Operations
- Array.`map` is used to perform a code block/method on each element of the Array. Array.`collect` is the alias for this method. ex

<pre><code class="ruby">
[1, 2, 3, 4, 5].map { |i| i + 1 } # returns [2, 3, 4, 5, 6]
</code></pre>
- Array.`select` filters elements of an array according to a boolean code block/method given as an argument.ex

<pre><code class="ruby">
names = ['rock', 'paper', 'scissors', 'lizard', 'spock']
names.select { |str| str.length > 5} # returns ["scissors", "lizard"]
</code></pre>
- Array.`delete(obj)` deletes all items from Array that are equal to obj.
- Array.`delete_if cond` deletes all items from Array that satisfy the given cond in the argument. ex

<pre><code class="ruby">
[1,2,3,4,5,6,7].delete_if{|i| i < 4 } # returns [4, 5, 6, 7]
</code></pre>

### 3.2 Iteration in Arrays.
- `for` loops with Arrays. For loops are not used very much in Ruby. ex
<pre><code class="ruby">
array = [1, 2, 3, 4, 5]
for i in array
  puts i
end
</code></pre>
- Array.`each block` runs the argument block for each element of Array. Array.`each` are de-facto loop standards in Ruby. ex.

<pre><code class="ruby">
array = [1, 2, 3, 4, 5]
array.each do |i|
  puts i
end
</code></pre>

### 4.0 Introduction to Ruby Hashes
- A __Hash__ is a collection of key-value pairs. You retrieve or create a new entry in a Hash by referring to its key. Hashes are also called 'associative arrays', 'dictionary', 'HashMap' etc. in other languages

- creating an hash: `{}` or `Hash.new` or `{1 => "one",2 => 12}`
- `[]` is used for fetching values from a Hash. The brackets enclose the key.
- Adding key-value pairs: `hash["key"] = "value"`

### 4.1 Hashes, in and out.
- Hash.`each block` is used to iterate over all elements of the hash. However unlike Array.`each`, it passes two values to the block: the key and the value of each element.
- [__Extra__] Number.`to_f` returns the float-version of the Number. By default, the division of int/int returns int.
- Hash.`keys` returns an array of all the keys in the Hash.
- Hash.`values` returns an array of all the values in the Hash
- Specifying a default in the Hash constructor will always return your custom default for any failed lookups on that hash instance. for ex, `Hash.new("default")` returns default for any failed lookups.
- The two shortcuts with `Hash::[]`.
  * In first one, Hash::[] takes a flat list of parameters, arranged in pairs, and then converts that into a Hash.
  * The second takes just one parameter: an array containing arrays which are themselves key-value pairs, and then converts that into a Hash.

<pre><code class="ruby">
chuck_norris = Hash[:punch, 99, :kick, 98, :stops_bullets_with_hands, true] #first_way
puts chuck_norris # returns {:punch=>99, :kick=>98, :stops_bullets_with_hands=>true}

def artax
  a = [:punch, 0]
  b = [:kick, 72]
  c = [:stops_bullets_with_hands, false]
  key_value_pairs = [a, b, c]
  Hash[key_value_pairs] # second way.
end
puts artax # returns {:punch=>99, :kick=>98, :stops_bullets_with_hands=>true}

</code></pre>

### 5.0 Classes
- One may look up the class of any object by simply calling the `class` method on it.
- Object.`is_a?(given_class)` returns true if the Object is an instance of the given_class.
- classes themselves are simply objects that belongs to the class `Class`.
- `1.class.class` returns `Class`.
- calling the `new` method on a class results in an instance being created.

### 5.1 Building your own class
- __CONVENTION__: classes in Ruby have names beginning with a capital letter.

__For a class to justify its existence, it needs to have two distinct features__:

__State__: A class must have some kind of state that defines the attributes of its instances. In the case of a simple rectangle, this could simply be its length and breadth.

__Behaviour__: A class must also do something meaningful. This is achieved by the programmer adding methods to the class that interact with its state to give us meaningful results.

- __CONVENTION__:  instance variables of the class, are part of the __state__ and have `@` in front of them.
- `initialize` method is the constructor of the class.


### 6.1 Being Methodical
- Data an object contains is _what it is_ and its methods are _what it can do_.
- Methods aren't exempt from Ruby's "everything is an object" rule. methods exposed by any object are themselves objects.
- All objects in Ruby expose a method `method` that can be used to get hold of any of its methods as an object.
- You can still call the method using the eponymous `call` method and it responds like a normal invocation of that method.
- Even a method that does nothing at all and has no return produces an object - the `nil`.
- The `return` exits the method; the `puts` statement that comes right after is never run.

<pre><code class="ruby">
puts 1.method("next") # returns the method object - #<Method: Fixnum(Integer)#next>
puts 1.method("next").call # calls the method object producing - 2

def do_nothing
end

puts do_nothing.class # an empty method returns nil object.
</code></pre>

### 6.2 Calling a method
- method arguments with default values.
<pre><code class="ruby">
def add(a_number, another_number = 0) # another_number has default value of 0.
  a_number + another_number
end
</code></pre>

- __splat operator (*)__: The splat operator is used to handle methods which have a variable parameter list. The parameter list passed to an object is available as a list with splat operator. The splat operator works both ways - you can use it to convert arrays to parameter lists as easily as we just converted a parameter list to an array.

<pre><code class="ruby">
def add(a_number, another_number, yet_another_number)
  a_number + another_number + yet_another_number
end

numbers_to_add = [1, 2, 3] # Without a splat, this is just one parameter
puts add(\*numbers_to_add)  # without the splat operator numbers to add wont be changed into a parameter list.
</code></pre>

- You can even mix parameter lists and splatting.
<pre><code class="ruby">
def add(\*numbers)
  numbers.inject(0) { |sum, number| sum + number }
end

def add_with_message(message, \*numbers)
  "#{message} : #{add(\*numbers)}"
end

puts add_with_message("The Sum is", 1, 2, 3)
</code></pre>

- Array.`join(delimiter)` creates a string delimited by the delimiter.
- Ruby allows the last parameter in the parameter list to skip using curly braces if it's a hash, making for a much prettier method invocation.


<pre><code class="ruby">
def add(a_number, another_number, options = {}) # putting the last parameter as {} allows it to be  a  
  sum = a_number + another_number
  sum = sum.abs if options[:absolute]
  sum = sum.round(options[:precision]) if options[:round]
  sum
end

puts add(1.0134, -5.568)
puts add(1.0134, -5.568, absolute: true)
puts add(1.0134, -5.568, absolute: true, round: true, precision: 2)
</code></pre>

- Another example.

<pre><code class="ruby">

def add(\*numbers)
  numbers.inject(0) { |sum, number| sum + number }  
end

def subtract(\*numbers)
  current_result = numbers.shift
  numbers.inject(current_result) { |current_result, number| current_result - number }  
end

def calculate(\*arguments)
  # if the last argument is a Hash, extract it
  # otherwise create an empty Hash
  options = arguments[-1].is_a?(Hash) ? arguments.pop : {}
  options[:add] = true if options.empty?
  return add(\*arguments) if options[:add]
  return subtract(\*arguments) if options[:subtract]
end

</code></pre>

### 7.1 Lambdas In Ruby
- a lambda is just a function, without a name. They're anonymous, little functional spies sneaking into the rest of your code.
- Lambdas in Ruby are also objects, just like everything else! The last expression of a lambda is its return value, just like regular functions.
- Lambdas take parameters by surrounding them with pipes.
- __CONVENTION__: Use {} for single line lambdas and do..end for lambdas that are longer than a single line.

<pre><code class="ruby">
increment = lambda {|x| x + 1 }
increment.call(2) # returns 3
</code></pre>

### 7.2 Blocks in Ruby

__Lambdas vs Blocks__
A __lambda__ is a piece of code that you can store in a variable, and is an object. The simplest explanation for a __block__ is that it is a piece of code that can't be stored in a variable and isn't an object. It is, as a consequence, significantly faster than a __lambda__, but not as versatile and also one of the rare instances where Ruby's "everything is an object" rule is broken.

- 'yield item' passes the item to the block associated with the method it resides in. `yield` keyword can call a single lambda that has been implicitly passed to a method without using the parameter list

### 8.1 Getting Modular
- __Modules__ only hold behaviour, unlike classes, which hold both behaviour and state.
- Since a module cannot be instantiated, there is no way for its methods to be called directly. Instead, it should be included in another class, which makes its methods available for use in instances of that class.
- In order to include a module into a class, we use the method `include` which takes one parameter - the name of a Module. example.

<pre><code class="ruby">
module WarmUp
  def push_ups
    "Phew, I need a break!"
  end
end

class Gym
  include WarmUp

  def preacher_curls
    "I'm building my biceps."
  end
end

puts Gym.new.push_ups # returns Phew, I need a break!

</code></pre>

- all modules in Ruby are instances of `Module`. `Module` is the superclass of `Class`, so this means that all classes are also modules, and can be used as such.

### 8.2 Modules as Namespaces
- Modules can also hold classes.

<pre><code class="ruby">
module Perimeter
  class Array
    def initialize
      @size = 400
    end
  end
end
</code></pre>

- We have these two classes alongside each other. This is possible because we've namespaced our version of the Array class under the Perimeter module.
- The real problem that namespacing solves is when you're loading libraries.
- When you're creating libraries with Ruby, it is a good practice to namespace your code under the name of your library or project.
- `::` is a __constant lookup operator__ that looks up the Array constant only in the Perimeter module.
- you can scope any constant using __constant lookup operator__(`::`) operator, not just classes.
- We can nest constant lookups as deep as we want. And, we aren't restricted to just classes and modules.
- If you prepend a constant with :: without a parent, the scoping happens on the topmost level.

### 9.1 Streams
- An __input/output__ stream is a sequence of data bytes that are accessed sequentially or randomly.
- Streams are like an abstract, high level concept.
- I/O streams are used to work with almost everything about your computer that you can touch, see, or hear.
- __pure__ code is code without side-effects: code which simply performs calculations.
- A __pure__ program isn't very useful if it can't even print its results to the screen! This is where I/O streams come in.

- IO.`sysopen(Filename, mode)` gives a file descriptor which can be used, with IO.`new` to create new IO objects as shown below:

<pre><code class="ruby">
# open the file "new-fd" and create a file descriptor:
fd = IO.sysopen("neee", "w")

# create a new I/O stream using the file descriptor for "new-fd":
p IO.new(fd)

</code></pre>

- The notion of creating a "file descriptor" is inherited from UNIX, where everything is a file.
- There are a bunch of I/O streams that Ruby initializes when the interpreter gets loaded. This is how to see them.

<pre><code class="ruby">
io_streams = Array.new
ObjectSpace.each_object(IO) { |x| io_streams << x }

p io_streams

</code></pre>

- Ruby defines constants `STDOUT`, `STDIN` and `STDERR` that are IO objects pointing to your program's input, output and error streams that you can use through your terminal, without opening any new files.
- You can see them with `STDOUT.class`, showing the class name and `STDOUT.fileno` showing the fileno.
- Whenever you call `puts`, the output is sent to the IO object that `STDOUT` points to. Same with `gets` to `STDIN`.
- The Kernel module provides us with global variables `$stdout`, `$stdin` and `$stderr` as well, which point to the same IO objects that the constants `STDOUT`, `STDIN` and `STDERR` point to.
- The purpose of these global variables is __temporary redirection__: you can assign these global variables to another IO object and pick up an IO stream other than the one that it is linked to by default.
- We can use the StringIO class to easily fake out the IO objects. here is how to capture STDERR so that calls to warn  are redirected to our costum stringIO object.

<pre><code class="ruby">
capture = StringIO.new
$stderr = capture
</code></pre>

### 9.2 Using the `File` Class
- Opening, reading, and inspect a file with `File` class.

<pre><code class="ruby">
mode = "r+"
file = File.open("friend-list.txt", mode)
puts file.inspect
puts file.read
file.close
</code></pre>

- `mode` is a string that specifies the way you would like your file to be opened, it can be 'r+' for read-write, 'w' for write-only, 'r' for read-only. other modes are listed [here](http://ruby-doc.org/core-1.9.3/IO.html).
- File.`open` also takes an optional block which will auto-close the file you opened once you are done with it.

<pre><code class="ruby">
what_am_i = File.open("clean-slate.txt", "w") do |file|
  file.puts "Call me Ishmael."
end

p what_am_i # Call me Ishmael.

File.open("clean-slate.txt", "r") {|file| puts file.read }
</code></pre>

- The File.`read` method accepts two optional arguments:`length`, the number of bytes upto which the stream will be read, and `buffer`, where you can provide a String buffer which will be filled with the file data.
- File.`rewind` rewinds the read file to the starting location so that it can be read again.
- File.`seek` lets you "seek" to a particular byte in the file to tell Ruby where you want to start reading from.
- File.`readlines` returns an array of all the lines of the opened IO stream.
- writing to a file with File.`write`

<pre><code class="ruby">
File.open("disguise", "w") do |f|
  f.write("Bar")
end
</code></pre>
