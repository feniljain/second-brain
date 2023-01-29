- It has something known has `atoms`, which are like global constants, which have value = their name, so `:foo` is an atom with foo as it's name and value as foo
	- Doubt: Does this go in global constants section of ELF?
- Lists in elixir are implemented using linked lists, so finding length will be an O(N) operation
	- And similarly prepending to a list is usually faster than appending
		- And the way you prepend is `["pi" | list]`
	- And the way you append is `list ++ ["Cherry"]
		- This seems like making a new list and appending that with old linked list
		- While prepending one seems like you are making a list by doing an `OR` of a variable and a list ( I actually tried to do this, and a `OR` between a string and a list is not possible xD )
	- Doubt: Why have such different syntax for append and prepend?
- It does have `nil` type
- It has a completely new string concat operator in the form of: `<>`
- It also allows comparison of 2 and 2.0, but has a javascript type `===` for stricter comparison
	- Actually in elixir you can compare any type to any other type, there is a precedence list showing which types take precedence over what
- It always returns float on using `/`  operator
	- For integer division, one needs to use `div()`
	- And for modulo, one needs  `rem()`
- It has this format of saying arity of an operator/function take and the name of the operator/function itself, something like: `<operator>/<arity>`. E.g. `++/2`
	- So question over here arises, what about variadic arguments? Are they not supported  like Rust? ( Doubt )
- You can subtract lists using `--/2`! Hmm....interesting
	- This is more like A-B which we have in sets
- In elixir, a list's tail means everything in a list except the first element
	- What!? So head = first element and tail = rest of the list
- So tuples seem to be stored stored contiguously in memory
- So elixir has one native supported data structure known as `Keyword lists`
	- These are lists of tuples of 2 size, out of which first is an atom ( this will be the key ) which does not need to be unique, so non-unique keys
		- And also keys are ordered
	- I am interested in seeing the uses of this data structure in various places. The reason which makes it good enough to be given a unique name and implemented natively
- Updating a map creates a completely new map, and note this updating so key should already be present in the map
- In Elixir, the `=` operator is actually a match operator, comparable to the equals sign in algebra.
	- So the syntax of `[ 1 | tail ] = list` , is a special case of pattern matching
	- So in cases of `foo = 1` , it acts as an assignment to a variable
	- But what if you want to match in this case too, for that we have `^` (pin) operator
	- So `=` is for single pattern, and `case` , `cond`, `with`, etc. are for multiple and ever complex pattern matching
- Only flasey values are `nil` and `false` ( so that's why `0 && true` will `true`)
- Elixir has a default `if not`  case, it's known as `unless`, i.e. it only gets triggered when the given condition after `unless` is false
- So one of the neat things I liked about pattern matching is it having in built support for `guard patterns`, so you can pattern match and then guard entry to that case
- `if else` in other language = `cond/1`  in elixir
- You know `with` reminds me of `?` in Rust, either give me the value or just return an error
	- Project: I wonder if I can implement a version of `with` such that, it even returns error
	  if  `nil` is returned. Could be an interesting project
	  - Project: Is function overloading possible in elixir? If yes, do it for the above project by overloading `with`s default functionality xD
		  - Got the answer yes, it is possible to overload the functions!
  - Elixir is a functional programming language and hence depends on functions a lot. So they have this shortcut for using them it's by using `&` and then for parameters you use something like we see in shell scripts, `&1`, `&2`, etc. Example conversion:
  
```elixir
sum = fn (a, b) -> a + b end
```
is equal to
```elixir
sum = &(&1+&2)
```

- Pattern matching on function signature is so lit!
- Elixir has so eye pleasing syntactic sugar, ofc pattern matching on function signature is a good idea, but also having special syntax for one line functions, it's nice.
 - Behind the scenes, functions pattern-match the data passed in to each of its arguments independently. We can use this to bind values to separate variables within the function.
	- They are really into this pattern-matching business, is this the case with Elixir only ( I know functional languages pattern matching a lot, but don't know to what extents ) or with majority of functional programming languages? ( Need to learn more of them to know ig :) )
- `|>` operator supremacy :bow:
- Doubt: Can attributes be compile time evaluated?
- Structs cannot be defined outside a module. Structs take name of module.
- I like how arity is so openly used even in the language syntax, we have syntax like:
```elixir
import List, except: [last: 1]
```
- This says language to not fetch function `last` which has arity = 1
- `use` is a very interesting keyword, if we think about the basic example from `elixirschool`, it's elixir's way to construct a module whose methods you wanna expose under your current module.
	- Doubt: This observation can be very wrong, but if it isn't, is there a way to selectively provide such constructors for different modules, like only exposing some functions for one use and only exposing another ones for another use statement
- Providing a REPL with all dependencies and code loaded from a project, this is so lit!
- _Atoms_ are internally represented by an integer in a lookup table, which are set automatically. It is not possible to change this internal value.
- Overall it's a dynamically typed language, but you can specify type spec of a function by using `@spec`, e.g.:
```elixir
@spec leap_year?(non_neg_integer()) :: boolean()
def leap_year?(year) do
	...
end
```
- Their LSP sucks big time!
- Elixir has two different structures, charlists and strings
	- Strings are denoted by `""`
	- Charlists are denoted by `''`
		- These are like lists and all lists operations can be performed on it
		- It is actually a list of unicode values of the character at a given position