# Getting Started with Elixir

> Updated 23rd Janaury 2017.

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

- **Tuples**

    - Ordered collections of 2-5 items. for more items, use List/Map.
    - Create a tuple like `book = {"programming with elixir", 51002, 90.19}`
    - To get 2nd element from the book tuple, `elem(book, 1)`
    - To change element at 3rd position of the book tuple, `put_elem(book, 2, "Newton Taylor")`
    - `put_elem` doesn't mutate the book tuple. Data is immutable in elixir.
    - `{title, price, author} = book`, matches the book tuple to the left hand side variables title, price and author. If you don't need any of the element from book, you can match it with `_`(underscore).

- **List**

    - Better data structure for big collection of data items.
    - In Elixir, Lists are singly linked. Each element has a pointer to the next element, but no pointer to the prev element. Prepending the easier than appending.
    - `hd(my_list)` gives the first element (head of the list), and `tl(my_list)` gives the list minus first element(tail of the list).
    - Prepending to the list: `[89 | my_list]`, prepends 89 to the my_list.
    - Patten matching left-side and right-side works in lists.

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

## Control Flow

- Branching logic: if, cond, case.
- Iterating logic: recursion, no loops.
