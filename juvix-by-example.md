# Juvix By Example

<!---
```juvix src/Package.juvix
module Package;

import PackageDescription.V2 open;

package : Package :=
  defaultPackage@{
    name := "juvix-by-example"
  };
 
```
--->

## Hello World

This is the source code of the traditional Hello World program.

```juvix src/HelloWorld.juvix
-- This is a comment, it is ignored by the compiler.
--
-- A Juvix file always starts with a module declaration.
module HelloWorld;

-- This line imports the standard library
import Stdlib.Prelude open;

-- The main function is run when the program is executed.
main : IO :=
    -- Print a String to standard out.
    printStringLn "Hello World!"
```

This program can be compiled into an executable using the `juvix compile` command:

```
$ juvix compile native HelloWorld.juvix
$ ./HelloWorld
Hello World!
```

Alternatively it can be evaluated with `juvix eval`:

```
$ juvix eval HelloWorld.juvix
Hello World!
```

## Literals

The Juvix standard library supports basic literals, Integers, Natural numbers (non-negative integers), Booleans, and Strings.

```juvix src/Literals.juvix
module Literals;

import Stdlib.Prelude open;

main : IO :=
  printStringLn ("Juvix" ++str "Anoma")
    >>> printNatLn (10 + 2)
    >>> printIntLn (2 * 100)
    >>> printBoolLn (true && false)
    >>> printBoolLn (true || false)
    >>> printBoolLn (not true);
```

```
$ juvix eval Literals.juvix
JuvixAnoma
12
200
false
true
false
```

## Variables

In Juvix you declare variables with `let ... in` syntax. Multiple variables can be defined in a single `let ... in` block.

```juvix src/Variables.juvix
module Variables;

import Stdlib.Prelude open;

main : IO :=
  let
    foo : String := "foo";
    bar : String := "bar";
    baz : String := "baz";
  in printStringLn (foo ++str bar ++str baz);
```

```
$ juvix eval Variables.juvix
foobarbaz
```

## If/Else

You can use `if` for branching in Juvix programs:

```juvix src/If.juvix
module If;

import Stdlib.Prelude open;

main : IO :=
  if
    | 7 < 0 := printStringLn "7 is negative"
    | 7 < 10 := printStringLn "7 has one digit"
    | else := printStringLn "7 has multiple digits";
```

```
$ juvix eval If.juvix
7 has 1 digit
```

## Functions

To define a function in Juvix we simply write the function name, its arguments and return type followed by the function body.

Functions are called using the name of the function followed by the parameters separated by spaces.

```juvix src/Functions.juvix
module Functions;

import Stdlib.Prelude open;

doubleMe (x : Int) : Int := x + x;

doubleTwo : Int := doubleMe 2;

main : IO := printIntLn doubleTwo;

```

```
$ juvix eval Functions.juvix
4
```

## Custom Data Types

Juvix custom data types are declared using the `type` keyword.

A _record_ is a collection of fields.


```juvix src/Records.juvix
module Records;

import Stdlib.Prelude open;

-- The `Person` record has `name` and `age` fields.
type Person :=
  mkPerson {
    name : String;
    age : Nat
  };

-- `mkPerson` constructs a `Person` record value.
alice : Person :=
  mkPerson@{
    name := "Alice";
    age := 42
  };

-- The functions `Person.name` and `Person.age` can be used to access the data in a record value.
main : IO :=
  printString "name: "
    >>> printStringLn (Person.name alice)
    >>> printString "age: "
    >>> printNatLn (Person.age alice);
```

```
$ juvix eval Records.juvix
name: Alice
age: 42
```
