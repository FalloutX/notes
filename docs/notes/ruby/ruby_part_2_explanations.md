## Some more Notes/Explantions on ruby.

> Last Updated on Oct 4th 2015.

##### `===` operator
- [x] READ [What does the “===” operator do in Ruby? | StackOverflow](http://stackoverflow.com/questions/4467538/what-does-the-operator-do-in-ruby)

- [x] READ [=== vs. == in Ruby | Stack Overflow](http://stackoverflow.com/questions/3422223/vs-in-ruby)

- Its called __subsumption operator__. So it its written `a === b`, then __subsumption operator__ is a boolean operator which asks the question "If I have a drawer labelled `a` would it make sense to put `b` in that drawer?"
- `a === b` means "If a described a set, would b be a member of that set?"

<pre><code class="ruby">
(1..5) === 3           # => true, since 3 belongs to the set of 1..5
(1..5) === 6           # => false

Integer === 42          # => true, since 42 is in set of all Integers
Integer === 'fourtytwo' # => false

 /ell/ === 'Hello'     # => true, Hello matches somewhat with the /ell/ regex.
 /ell/ === 'Foobar'    # => false

</code></pre>

- The main usage for the === operator is in case expressions.

<pre><code class="ruby">
case foo
when bar  # here actually a === is happening, so we can replace bar with a
  baz     # set, and foo with any member of that set.
when quux
  flurb
else
  blarf
end
</code></pre>


- Note that if you want to search for this operator, it is usually called the __triple equals operator__ or __threequals operator__ or __case equality operator__. They are definitely misleading since `===` has nothing to do with equality.
- For `===` there is no expectation of either symmetry or transitivity. In fact, it is very much by design not symmetric.

#### Reflection Methods in Objects.
- Methods like `is_a?` or `.class`, which tell you something about the object itself are called __Reflection Methods__.

#### Bang Methods.
- __Bang Methods__ are finished with an exclamation point `!` like `#sort!`, and they actually modify the original object. The exclamation point lets you know you're in dangerous territory.
- Chaining a bunch of methods together is called __Method Chaining__.

#### `nil`
- It represents nothing... literally. Before you assign a value to something, it starts as nil. for ex.

<pre><code class="ruby">
my_arr = []
#=> []
my_arr[3]
#=> nil     
</code></pre>
- Sometimes you want to know if a value or variable is nil before doing something. Use the method `nil?` to ask whether a given object is nil or not.

<pre><code class="ruby">
nil.nil?
#=> true
[].nil?
#=> false        # Array is empty but not nil.
</code></pre>

- If you want to check whether an array or someother object is empty or not, use `empty`.

#### `p` vs `puts`
- `p` will give you some more information because it runs the `#inspect` method on the object while `#puts` runs the `#to_s` method.
- `inspect` is supposed to impformative while `to_s` is supposed to be pretty.

#### working with dates and times.
- Ruby uses the `Time` class to let you work with dates and times, giving you some handy methods to find out about specific parts.
- `Time.now` gives the current time. same for `Time.new`.

<pre><code class="ruby">
my_time = Time.now
#=> 2015-09-10 03:33:15 +0530
my_time.year
#=> 2015
my_time.month
#=> 9
my_time.day
#=> 10
my_time.wday
#=> 4                # the day of the week, starting Sunday
my_time.hour
#=> 3
my_time.min
#=> 33
my_time.sec
#=> 15
</code></pre>

- `Time` also takes inputs if you want to create a specific time, from year to time zone:

<pre><code class="ruby">
Time.new(2012,2,14)
#=> 2012-02-14 00:00:00 -0800
</code></pre>

- You can add and subtract times just like they were numbers, since they are just seconds from Jan 1, 1970.

<pre><code class="ruby">
vday = Time.new(2012,2,15)    # Valentine's Day!
#=> 2012-02-14 00:00:00 -0800
vday+3600                     # 1 hour's worth of seconds
#=> 2012-02-14 01:00:00 -0800
xmas = Time.new(2015,12,25)
#=> 2013-12-25 00:00:00 -0700    # Xmas!
(( xmas - Time.now )/60/60/24).to_i
#=> 105                          # Until Xmas!
</code></pre>

- Formating the Time String.

<pre><code class="ruby">
nownow = Time.now
#=> 2013-07-10 17:37:27 -0700
nownow.ctime                  # a standard display type
#=> "Wed Jul 10 17:38:10 2013"
nownow.utc                    # Remove the time zone
#=> 2013-07-11 00:38:10 UTC
nownow.strftime("%Y-%m-%d %H:%M:%S") # This function is important.
#=> "2013-07-11 00:38:10"
</code></pre>

#### `nil?` vs `blank?` vs `empty?` [Stack Overflow]

- [x] READ [A concise explanation of nil v. empty v. blank in Ruby on Rails | Stack Overflow](http://stackoverflow.com/questions/885414/a-concise-explanation-of-nil-v-empty-v-blank-in-ruby-on-rails)

- `.nil?` can be used on any object and is true if the object is nil.
- `.empty?` can be used on strings, arrays and hashes and returns true if:
    * String length == 0
    * Array length == 0
    * Hash length == 0
- `.empty?` on something that is nil will throw a `NoMethodError`
- `.blank?`(Rails Only) - will operate on any object as well as work like `.empty?` on strings, arrays and hashes. Won't throw error on nil objects.
- `.blank?` also evaluates true on strings which are non-empty but contain only whitespace.
- `.present?`(Rails Only) - is the opposite of the `.blank?`
- Array gotcha: `.blank?` will return false even if all elements of an array are blank. To determine blankness in this case, use `all?` with `blank?`.
