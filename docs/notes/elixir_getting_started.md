# Getting Started with Elixir

> Updated 25th Janaury 2017.

## Elixir Data Types.

- **Numbers** - (no upper range)

    - [Integer](https://hexdocs.pm/elixir/Integer.html)
    - [Float](https://hexdocs.pm/elixir/Float.html)

- **Atoms** (called symbols in Ruby) - `:firstname` is an atom. `:ok` and `:error` are very common atoms in elixir. | [Atoms](https://hexdocs.pm/elixir/Atom.html)

    - Elixir doesn't have a Boolean type. Instead it uses `:true` and `:false` atoms.
    - Atoms are more memory efficient than strings.
    - `:nil`, `:false`, `:true` can be used without colons at the start, like `nil`, `false`, `true`.

- **Strings** are UTF-8 out of the box. | [Strings](https://hexdocs.pm/elixir/String.html)

    - `<>` is the concatenation operator.

    - `"hello" <> " world!"` becomes `"hello world!"`

    - String Interpolation is done with `"#{}"`

    - `"Hello, #{'andy'}"` becomes `"Hello, andy"`

    - Keep in mind single-quoted and double-quoted representations are not equivalent in Elixir. Single quotes are char lists, double quotes are strings.

- **Tuples**

    - Ordered collections of 2-5 items. for more items, use List/Map.
    - Create a tuple like `book = {"programming with elixir", 51002, 90.19}`
    - To get 2nd element from the book tuple, `elem(book, 1)`
    - To change element at 3rd position of the book tuple, `put_elem(book, 2, "Newton Taylor")`
    - `put_elem` doesn't mutate the book tuple. Data is immutable in elixir.
    - `{title, price, author} = book`, matches the book tuple to the left hand side variables title, price and author. If you don't need any of the element from book, you can match it with `_`(underscore).
    - Tuples store elements contiguously in memory. This means accessing a tuple element by index or getting the tuple size is a fast operation.

- **List**

    - Better data structure for big collection of data items.
    - In Elixir, Lists are singly linked. Each element has a pointer to the next element, but no pointer to the prev element. Prepending the easier than appending.
    - `hd(my_list)` gives the first element (head of the list), and `tl(my_list)` gives the list minus first element(tail of the list).
    - Prepending to the list: `[89 | my_list]`, prepends 89 to the my_list.
    - Patten matching left-side and right-side works in lists.
    - Two lists can be concatenated or subtracted using the `++/2` and `--/2` operators.

- **Immutablity**

    - In elixir data is immutable, once a list/tuple is created it cannot be modified.
    - Immutability helps with concurrency in elixir.
    - Efficient Memory Use. It knows the memory assigned cannot be modified, so elixir doesn't have to copy stuff.

- **Maps**

    - Collection of key-value pairs, keys don't have to be atoms. Only one instance of a key is allowed.
    - syntax - `%{ 1 => {"Nate", "nate@gmail.com"}, 2 => {"charles", "charles@gmail.com"} }`
    - Even tuples can be used as keys for maps.
    - If they key is an Atom, then you can use dot syntax to access that property, like `costumers.nate`, else for other you need to use `[]` syntax, like `costumers['charles']`.

## Modules & Functions

- **Modules**

    - Elixir used do-end blocks instead of curly braces or indents.

    ```elixir
    defmodule ExampleModule do
      # Module Code.
    end
    ```

- **Module Directives**

    - `import` to import other modules into the current module.
    - `import IO, only: [puts: 1]` will only import `puts` function from the IO Module.
    - `import Kernel, except: [inspect: 1]` will import everything from `Kernel` module except the `inspect` function.
    - `alias ModulePlayground.Misc.Util.Math, as: MyMath` will add `MyMath` alias for rather long name of `ModulePlayground.Misc.Util.Math`. If `as:` option in not provided, it would use the last name of the aliased Module as the alias. For `ModulePlayground.Misc.Util.Math`, the alias without `as:` would be `Math`.
    - `require` is used to bring in Macros from other modules into your module.

- **Basic Operators**
    - __Arithmetic Operators__: `*`, `+`, `/`, `-`, `div/2`(for integer division) & `rem/2`(remainder)
    - List Concatenation (`++`) and List Subtraction `--`.
    - String Concatenation `<>`
    - __Boolean Operators__(strict): `and`, `or` and `not`. they expect boolean as a first argument.
    - __Boolean Operators__(non-strict): `&&`, `||` and `!`. don't expect boolean as a first argument. only `false` & `nil` are falsy in Elixir
    - __Comparision__: `==`, `!=`, `===`, `<=`, `>=`, `>` and `<`.
    - `===` vs `==`: `===` is more strict when comparing floats and integers. `1 === 1.0` is `false`, while `1 == 1.0` is true.
    - In Elixir, different data types can be compared. `1 < :atom` is true.
    - Data Types Sorting Order: `number < atom < reference < function < port < pid < tuple < map < list < bitstring`


- **Functions**

    ```elixir
    defmodule Sample do # The module that encloses the function

        def SampleFunction do
            #Function code.
        end

    end
    ```

    - last evaluated statement is the default return value of the function, like Ruby.

    - **Function Arity** - {function name}/{number of parameters}

    - Shorthand for writing smaller functions.

    ```elixir
    def first([]), do:nil
    def first([head | _]), do: head
    ```

    ​

- **Gaurd Clauses**

    - To safely return sane results when inputs are bit worse than expected, and keep such inputs from entering the saner/more logical function.

    - Guard Clause way to do the above functionality.

    ```elixir
    def first(list) when length(list) == 0, do: nil #This would execute when list is empty.

    def first([head | _]), do: head
    ```

- **Default Parameters**

    - Specify default parameter with `\\`(double backslash) symbol. In the below example, `val` has a default value of 0.

    ```elixir
    def prepend(list, val \\ 0) do
        [val | list]
    end
    ```

- **Private Functions**

    - To define a private function, use the defp macro instead of def macro used to define public functions.
    - Private Function would be accessible to other functions inside the module it was defined, but not outside.

    ```elixir
    defp trace(string) do
        IO.puts "The Value passed to trace is #{string}"
    end
    ```

- **Functions as first class citizens**

    - _passing a function as an argument_: Need to prefix `&` for capturing and suffix the function with its Arity.
    - _return functions as values from other functions_
    - _assign functions to a variable_

    ```elixir
    # passing a function as an argument
    Enum.map(list, &Sample.Utils.sqaure/1)

    # assign to a variable
    sqaure = &Sample.Utils.sqaure/2
    ```

- **Anonymous Functions**

    - to define a anonymous function with `fn` syntax
    - __Note__: a dot (`.`) between the variable and parentheses is required to invoke an anonymous function.
    - Therefore, Elixir makes a clear distinction between anonymous functions and named functions.
    - Anonymous functions are closures and as such they can access variables that are in scope when the function is defined

    ```elixir
    Enum.map(list, fn(x) -> x*x end)
    ```

    - using `&` capturing syntax

    ```elixir
    Enum.map(list, &(&1 * &1))
    #&1 captures the first argument

    Enum.reduce(list, 0, &(&1 + &2))
    # &n captures the nth argument.
    ```

- **Calling the passed function**

    - call the pass function `f` with `a` argument as `f.(a)`

- **Pattern Matching**
    - In Elixir, the `=` operator is actually called the match operator. When the sides of `=` do not match, a MatchError is raised.
    - Match operator is also useful for destructuring complex data types.

    ```elixir
    iex> {a, b, c} = {:hello, "world", 42}
    {:hello, "world", 42}
    iex> a
    :hello
    iex> b
    "world"
    ```

    - A list also supports matching on its own head and its tail.

    ```elixir
    iex> [head | tail] = [1, 2, 3]
    [1, 2, 3]
    iex> head
    1
    iex> tail
    [2, 3]
    iex> [h | t] = []  # head-tail matching won't work for an empty list
    ** (MatchError) no match of right hand side value: []
    ```
    - __Pin operator__ `^` can be use to pattern match against an existing variable’s value rather than rebinding the variable.

    ```elixir
    iex> x = 1
    1
    iex> ^x = 2 # Trying to match 1 = 2, will throw Match Error
    ** (MatchError) no match of right hand side value: 2
    ```
    - __Note__: You cannot make function calls on the left side of a match.


## Control Flow in Elixir

- Branching logic: if-else, cond, case.

- Iterating logic: recursion, no loops.

- **If-Else**

    ```elixir
    ## first functon with If Else

    def firstIF(list) do
        if length(list) == 0 do
            nil
        else
            hd(list)
        end
    end
    ```

- **Unless** - for the negative condtion instead of If.

    ```elixir
    def firstUnless(list) do
    	unless length(list) == 0 do
    		hd(list)
      end
    end
    ```

    - `quote EXP` prints out the Abstract syntax tree for evaluating the EXP.

- **Cond** macro

        ```elixir
        #Getting Day Abbreviation using the cond macro.
        def day_abbreviation(day) do
            cond do
                day == :Monday -> "M"
                day == :Tuesday -> "Tu"
                day == :Wednesday -> "W"
                day == :Thursday -> "Th"
                day == :Friday -> "F"
                day == :Saturday -> "Sa"
                day == :Sunday -> "Su"
                true -> "Invalid Day"
            end
        end
        ```

- **Case**


    -   Case statements are really useful combined with Pattern Matching capabilities of Elixir.
    -   You can also combine Gaurd Clauses with case statements for narrowing down cases.

    ```elixir
    def describe_date(date) do
        case date do
            {1, _, _} -> "Brand New Month!"
            {25, 12, _} -> "Merry Christmas"
            {25, month, _} -> "Only #{12-month} months until Christmas!"
            {31, 10, _} -> "Happy Halloween"
            {_, _ , _} -> "Just an average day!"
        end
    end
    ```

## Recursion in Elixir

> To understand what recursion is, you must first understand recursion.


- Writing a map function with Recursion.

```elixir
def map([], _), do: []
def map([head | tail], f) do
    [f.(head) | map(tail, f)]
end
```




- **Tail Recursion**

    - only happens when the last operation a function performs is recursion.

```elixir
# tail_map written with tail recursion instead of Recursion.
# also need reverse method to reverse the result.

def reverse(list), do: reverse(list, [])
def reverse([], reversed), do: reversed
def reverse([hd | tl], reversed), do: reverse(tl, [hd | reversed])


def tail_map([hd | tl], f), do: tail_map(tl, f, [f.(hd)])
def tail_map([], _, result), do: reverse(result)
def tail_map([hd | tl], f, result), do: tail_map(tl, f, [f.(hd) | result]
```

## Elixir Ecosystem.

- __Basics__: Mix - Build Tool & Hex - Package Manager.

- **Mix** - Task Runner, Build Tool for Elixir.
    - [Mix | Elixir School](https://elixirschool.com/lessons/basics/mix/)
    - [Introduction to Mix](http://elixir-lang.org/getting-started/mix-otp/introduction-to-mix.html)
    - `mix help` to list all the mix commands.
    - `mix local.hex` to install hex - package manager.

- **`mix new`**
    - for scaffolding a new elixir application.
    - `mix new app_name --sup` creates a new elixir application named `app_name` w/ supervisor. `app_name` needs to be in snake_case.

- **Supervisors & Umbrellas**
    - **Supervisor** process is only responsible for supervising other processes in the application and restart them if they crash.
    - **Umbrella** project is the one which has other elixir projects underneath it. A Grouping of similar elixir apps bundled into a single project.

- **Hex** - [Website](https://hex.pm/)
    - The package manager for Elixir Ecosystem.
    - `mix.exs` files's `deps` function contains the dependencies list.
    - `mix deps.get` to fetch and install the dependencies.

## Creating an Application.

- **Project Structure**
    - `mix.exs` - `project` function contains config of the project like elixir version, project version, dependencies etc. `application` function contains the other applications that need to be started for our application to get started.
    - `lib` folder contains our application code as well as our application module.
    - `config` folder holds files that are used for config properties.
    - `deps` folder is where dependencies get installed.
    - `test` is the conventional folder for your tests.

- **A Short Description of the Application**
    - This Application will read lines from a file, choose a random line and send that line as a tweet.

- **FileReader Module**
```elixir

# This Reads a file, and returns a random line from the file.
defmodule MyFirstApp.FileReader do
    def get_strings_to_tweet(filepath) do
        File.read!(filepath)
        |> String.split("\n")
        |> Enum.map(&String.trim/1)
        |> Enum.filter(&String.length(&1) <= 140)
        |> Enum.random()
    end
end

```

- **Tweet Module**

```elixir
defmodule MyFirstApp.Tweet do
    def send(str) do
        # Configure the Extwitter Module for accessing twitter.
        ExTwitter.configure(:process, [
            consumer_key: System.get_env("ELIXIR_APPS_TWITTER_CONSUMER_KEY"),
            consumer_secret: System.get_env("ELIXIR_APPS_TWITTER_CONSUMER_SECRET"),
            access_token: System.get_env("ELIXIR_APPS_TWITTER_ACCESS_TOKEN"),
            access_token_secret: System.get_env("ELIXIR_APPS_TWITTER_ACCESS_SECRET")
            ])
        # Send tweet.
        ExTwitter.update(str)
    end

    def send_random(file) do
        # this would send a random line from a file as a tweet.
        MyFirstApp.FileReader.get_strings_to_tweet(file) |> send
    end
end
```

- **Behaviours**
    - Defines a set of functions to be implemented.
    - Ensure that a module implements ALL functions in that set.
    - More like Interfaces in traditional OO languages.

- **Creating a Tweet Server**
    - Using GenServer, which is a behaviour in Elixir.

```elixir

defmodule MyFirstApp.TweetServer do
  use GenServer # GenServers are behaviours in Elixir

  def start_link() do
    # hardcoding the name of the server
    # start_link will call init.
    GenServer.start_link(__MODULE__, :ok, name: :tweet_server)
  end

  def init(:ok) do
    {:ok, %{}}
  end

  def handle_cast({:tweet, tweet}, _) do
    # Async
    # handle_call is sync.
    MyFirstApp.Tweet.send(tweet)
    {:noreply, %{}}
  end

  def tweet(tweet) do
    # This will call handle_cast above
    GenServer.cast(:tweet_server, {:tweet, tweet})
  end

end

```

- **Adding Tweet Server in Supervision Tree**
    - Add TweetServer in the supervision children list in `start` function of the application.ex

    - __File__: lib/my_first_app/application.ex

```elixir
def start(_type, _args) do
  import Supervisor.Spec, warn: false


  children = [
    worker(MyFirstApp.TweetServer, []) # Adding TweetServer in the supervision tree.
  ]

  opts = [strategy: :one_for_one, name: MyFirstApp.Supervisor]
  Supervisor.start_link(children, opts)
end
```

- **TweetServer processes**
    - `Process.whereis(:tweet_server)` to get the process ID of the tweet_server. This is not a OS process ID, but elixir process ID.
    - `Process.whereis(:tweet_server) |> Process.exit(:kill)` to kill the tweet server.
    - But since tweet server is in the Supervision tree, it'll be started again after we killed it.

- **Schedule Sending Tweets**

```elixir
defmodule MyFirstApp.Scheduler do
  def schedule_file(schedule, file) do
    Quantum.add_job(schedule, fn -> MyFirstApp.FileReader.get_strings_to_tweet(file)
    |> MyFirstApp.TweetServer.tweet end)
  end

end
```

- **Adding Scheduler to the start of the applicaiton**

    - modifying the `start` function in the `application.exs` file.

```elixir

def start(_type, _args) do
  import Supervisor.Spec, warn: false

  # Define workers and child supervisors to be supervised
  children = [
    # Starts a worker by calling: MyFirstApp.Worker.start_link(arg1, arg2, arg3)
    worker(MyFirstApp.TweetServer, [])
  ]

  # See http://elixir-lang.org/docs/stable/elixir/Supervisor.html
  # for other strategies and supported options
  opts = [strategy: :one_for_one, name: MyFirstApp.Supervisor]
  process = Supervisor.start_link(children, opts)
  MyFirstApp.Scheduler.schedule_file("*/5 * * * *",
  Path.join("#{:code.priv_dir(:my_first_app)}", "Sample.txt"))

  process
end
```

## Testing Elixir

- `mix test` to run the tests
- `mix test FILEPATH` to run the tests located at the `FILEPATH`.
- `mix test --only TAGNAME` to run the test tagged `TAGNAME`.

```elixir
# Tagging a test
@tag watching: true
test "this test will fail" do
  assert 2 + 3 == 5
end
```

- **ExUnit**
    - `use ExUnit.Case` needs to be in every Test Module.
    - Try to mimick directory structure of the app in the tests folder.

- **Testing File Reader Module**

    - Updated File Reader Module
```elixir
# lib/my_first_app/file_reader.ex

defmodule MyFirstApp.FileReader do
  # Divided the module into two parts, one that reads the file and other that picks the string, to improve testability.
  def get_strings_to_tweet(filepath) do
    File.read!(filepath)
    |> pick_string
  end

  def pick_string(str) do
    str
    |> String.split("\n")
    |> Enum.map(&String.trim/1)
    |> Enum.filter(&String.length(&1) <= 140)
    |> Enum.random()
  end
end
```

    - Tests for File Reader Module
```elixir
# test/my_first_app/file_reader_test.exs

defmodule FileReaderTest do
  use ExUnit.Case

  import MyFirstApp.FileReader
  test "Passing a file should return a string" do
    str = get_strings_to_tweet Path.join "#{:code.priv_dir(:my_first_app)}", "Sample.txt"

    assert str != nil
  end

  test "Will not return a line longer than 140 chars" do
    str = get_strings_to_tweet Path.join "#{:code.priv_dir(:my_first_app)}", "too_long.txt"
    IO.puts str
    assert str == "short line"
  end

  test "An Empty string should return an empty string" do
    str = pick_string ""

    assert str == ""
  end
end
```

- **Mocking out File Reader**
    - By Default, `ExUnit` doesn't have mocking ability baked in.
    - Mocking allows us to intercept calls to a specific module and redirect them to a function we wrote for testing.
    - You can use [**Mock Library**](https://hex.pm/packages/mock) to perform mocking.
    - `with_mock` is the main mocking function in Mock Library.
    - You can use [**Mix Test Watch Library**](https://hex.pm/packages/mix_test_watch) to automatically run tests when the some file changes occur. Command for that is `mix test.watch`
    - Example mocking the File Module
```elixir
test "The string returned should be trimmed" do
  with_mock File, [read!: fn(_) -> " ABC " end] do
    str = get_strings_to_tweet "doesnt_exist.txt"

    assert str == "ABC"
  end
end
```

- **DocTest**
    - A way of putting basic module tests in the docstrings of the module.
    - docstrings start with `@doc """` and end with `"""`
    - You can write doctest by writing the call to the function after `iex> ` and expected value in the next line.
    - To run doctest write `doctest MODULE` in the test file.

```elixir
# lib/my_first_app/file_reader.ex

defmodule MyFirstApp.FileReader do

  @doc """
  This Function will take the path to a file and return a string that can be
  tweeted out

  The Following is a DocTest

  iex> MyFirstApp.FileReader.get_strings_to_tweet "priv/doc.txt"
  "ABC"
  """


  def get_strings_to_tweet(filepath) do
    #...
  end
  #...
end
```

## Next Steps

- **Reference**
    - [Elixir Syntax Crash Course](http://elixir-lang.org/crash-course.html)
    - [Elixir Guides](http://elixir-lang.org/getting-started/introduction.html)
    - [Elixir Official Docs](https://hexdocs.pm/elixir/)
    - [Elixir Quick Reference](https://github.com/itsgreggreg/elixir_quick_reference)

- **Learning More of Elixir**
    - [Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)
    - [Elixir School](https://elixirschool.com/)
    - [Exercism.io Elixir Problems](http://exercism.io/languages/elixir/about)

- **Tools**
    - [Credo - Static Code Analysis tool](https://github.com/rrrene/credo) - like linters in other languages.

- **Resources**
    - [Elixir Status](https://elixirstatus.com/) - posts/blogs and other content related to elixir.
    - \#myelixirstatus on twitter.
    - [Elixir Fountain Podcast](https://soundcloud.com/elixirfountain)
    - [Elixir Conf 2016](https://www.youtube.com/watch?v=_O-bLuVhcCA&list=PLE7tQUdRKcyYoiEKWny0Jj72iu564bVFD)

- **Explanations**
    - [Why are there two kinds of functions in Elixir?](http://stackoverflow.com/questions/18011784/why-are-there-two-kinds-of-functions-in-elixir)
