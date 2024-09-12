- :: is read as "has the type of"
- two types of polymorphism:
	- parametric polymorphism
		 - also known as generics
	- constraint/ad-hoc polymorphism
- Haskell has ADT (Algebraic Data Types)
	- Sum Types, e.g.: data MyBool = MyFalse | MyTrue
	- Product Types, e.g. data Circle Float Float Float
- Think of ADT types in terms of set cardinality
	-  Cardinality of tuple (a, b) (tuple is a product type) will be (cardinality of a * cardinality of b)
	-  Sum types of MyBool = MyTrue | MyFalse = 1 + 1 = 2
		- Another e.g. is MyType = a | b = cardinality of a + cardinality of b
	- Cardinality of data Count = One Int | Two Bool will be (cardinality of Int) (zero to 2 power <whatever>, lets call it n which in general cases would be **2,147,483,647**) + (cardinality of Bool i.e. two) = n + 2
- If two types has same cardinality then they are considered `isomorphic` types
 
```
We usually use ' to either denote a strict version of a function (one that isn't lazy) or a slightly modified version of a function or a variable. Because ' is a valid character in functions, we can make a function like this.

> conanO'Brien = "It's a-me, Conan O'Brien!"
```

- functions can't begin with uppercase letters
- When a function doesn't take any parameters, we usually say it's a _definition_ (or a _name_).
- lists are a _homogenous_ data structure
- strings are just lists of characters
- prepend to list: `:` and append to list: `++`
- If you want to get an element out of a list by index, use `!!`
	- Wait why would they give an unsafe option such as this!?
 - Lists can be compared if the stuff they contain can be compared. When using <, <=, > and >= to compare lists, they are compared in lexicographical order. First the heads are compared. If they are equal then the second elements are compared, etc. 
 - `null` checks if a list is empty, preferred instead of using `l == []`
 - step in ranges:
 ```
 >[1,4..20]
  [1,4,7,10,13,16,19]
```

- Constraint in the end means it will return same type class instance, like `Num` has `Num :: * -> Constraint`, here it means `Num` on any operation can only return itself, which covers `Int`, `Float`, `Double`, etc. Try `:k Num Int` for this.

- `f :: Num a => a -> a -> a` this tells us, `f` function takes `a` which will have type class constraint of `Num`, we can also have more type class constraints like `Eq`. And then after `=>` we have the function body, `a -> a -> a`, takes two params of same type and returns a result of same type. In this case `f` was actually `(+)`.

- All functions in haskell are curried under the hood
```
f1 :: Integer -> Integer -> Integer
f1 = \a -> \b -> (+) a b
f1 a b = (+) a b -- This function is a syntactic sugar for last line
```

- In `:i Fractional` it shows: `class Num a => Fractional where ...`, `class Num` means Num is a super class of Fractional
- For `newtype` compiler gives an error when underlying type like `String` in case of `newtype MyStr = String` is passed to a place taking `MyStr`. While compiler will not contain in case of type alias, like `type MyStr = String`

```
`data Foo = Foo Int`: `Foo` and `Int` totally different.

`newtype Foo = Foo Int`: `Foo` and `Int` different at compile time but same at runtime.

`type Foo = Int`: `Foo` and `Int` same at compile time and runtime.
```

- Difference between data, newtype and type: https://www.reddit.com/r/haskell/comments/6xri4d/whats_the_difference_between_newtype_type_and_data/
- use `sprint` to understand how much has compiler evaluated something, try 

- `Int` type is bounded and `Integer` type is unbounded i.e. can hold any number, however big, without decimal points
- `If a function is comprised only of special characters, it's considered an infix function by default. If we want to examine its type, pass it to another function or call it as a prefix function, we have to surround it in parentheses.`
	- And that's why for checking type of operators like add, we have write: `:t (+)`
 
 - Generics in other languages = type variables in Haskell
 - `Everything before the => symbol is called a class constraint.`
 - If a pattern match in list comprehension fails, it moves on to next element.

- Normal Form -> Completely evaluated
- Weak headed Normal Form -> List hasn't been fully realized/evaluated

-   foldl = [] acc
    foldl = f (f acc x) xs
- foldr (f, acc, x:xs) = f x (foldr f acc xs)

- `*` in kind signature does not represent polymorphic type, it represents presence of type instead
		`data Trivial = Trivial'` has kind of `* -> *`
		`data Maybe a = None | Just a` also has kind of `* -> *`
	- Haskell cannot represent dependent types by default, and has no way of saying that when a `*` is present it may or may not take a polymorphic type

- type constructors are executed at compile time and data constructors are executed during runtime
- we can't have same named record type fields in same scope

- A set is closed  under an operation if applying that operation on any two elements in the set, produces a result in the same set. * : A x A -> A
- Magma: a set with a closed binary operation
- A magma where operation is associative is semigroup
	- associate: a * (b * c) == (a * b) * c
- A semigroup with an identity element (which is both left and right identity i.e. a * i == i * a == a) is monoid
- A monoid that has inverses relative to operation is group
	- It is a binary associative operation with an identity

- Functors don't change the structure, just the values. One example of structure is `List`
	- For something to be a functor it needs to a HKT
- fmap (f . g) == fmap f . fmap g
- Number of fmaps tell how many structures to go deep in and then apply the function