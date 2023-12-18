```
################################################################################
# comments
################################################################################

# comment

#[
    block comment
]

## doc comment outside

#! doc comment inside

##[
    block doc comment outside
]

#![
    block doc comment inside
]

################################################################################
# functions
################################################################################

# function
func name (a: u8, b: u16) u32 =
;;

# generics
func name <A: Eq + Ord> => (a: A) =
;;

# Higher kinded types
# most types have a kind of (*)
# a type that has generics has a kind of (* -> *)
# more generics is more stars (*, * -> *)
# nested kinds are possible ((*, * -> *) -> *)
# the default kind of generics is (*)
func name <A: (* -> *), T: Eq> => (input: A<T>) =
;;

# generic packs
# the example makes a tuple of different types
# this is done with the pack bound and the unpack keyword
# what this means is that A cannot be treated as a normal type anymore
# it can only be used in the context of unpack
func name <A: pack + Eq> => (input: (unpack A))

# genric packs can specify a minimum and maximum number of types
func name <A: pack(min: 2, max: 5)> => (input: (unpack A)) =
;;

# generics can have default values
func name <A: Eq = u8> => (input: A) =
;;

# compile time constants can be specified using the let keyword and a type
func name <let array_len: usize> => (input: [array_len]u8) =
;;
# or with default value
func name <let array_len: usize = 5> => (input: [array_len]u8) =
;;

# kind packs
# if the arity of the kinds is higher or lower than the parameter pack
# there will be a compile error
func name <A: (pack(min: 3, max: 5) * -> *), B: pack> => (input: A<unpack B>)

# calling a function
# lets say we have the following function:
func name <
    A: (pack * -> *),
    B: pack,
    let c: usize
> => (input: [c]A<unpack B>) =
;;
# to call this function you do the following:
func name<A = Either, B = (u8, u16), c = 2>( [Either::Right(200), Either::Left(300)] )
# most of the types can be inferred by the compiler so this can be rewritten like this:
func name( [Either.Right(200), Either.Left(300)] )

################################################################################
# types
################################################################################

# the type keyword exist to assign a name to a type
# using the regular type keyword you get a distinct name,
# that means that even if the types are structurally the same,
# the types are not equal
type name = type_expression;

# if you don't want that behavior, you need to add the alias keyword
# this means that it is literally an alias for the type
# so it doesn't become distinct
type alias = type_expression;

# record
type name = record {
    field1: u8,
    field2: u8
};;

# tuple
# a tuple iis 
type name = (u8, u16);;

# sum type
type name = sum
    | Name1 of u8
    | Name2 of u16
    | Name3 
;;

# array
# this is an array of five u8's
type name = [5]u8;;
# this is an array of five arrays of five u8's
type name = [5][5]u8;;

# pointer types
# []T # slice of T, fat pointer containing ptr and len
# ^T # pointer to T

# constructing slice
# slice syntax:
# T[0..4] # makes slice of type T of len 4 of elements 0 through 4

# constructing pointer
# pointer taking syntax:
# &T
# pointer deref syntax:
# T.*

# pointers cannnot be null and as such cannot be used across ffi boundaries
# to fix this use nullable pointer syntax
# ^?T

# literals
# record
let record_lit = name {field1: 2, field2: 6};
# tuple
let tuple_lit = (2, 8);
# sum literal
let sum_lit = name.Name1(5);
# array literal
let array_lit = [1, 2, 3, 4, 5];

# integer literal
1; 0xF;
# floating point literal
1.1; 0xF.F

# string literal
"Hello World";
# raw string literal
r"Hello World"; r#"Hello World"#;
# byte string
b"Hello World";
# raw byte string
br"Hello World"; br#"Hello World"#;
# c string (null terminated)
c"Hello World";
# raw c string
cr"Hello World"; cr#"Hello World"#
# null terminated byte string
cb"Hello World";
# raw null terminated byte string
cbr"Hello World"; cbr#"Hello World"#;

# char literal (unicode code point)
'A'
# char literals can have the same prefixes as string literals

# type generics
# same syntax as with function generics

type name <T> = T;

################################################################################
# variables
################################################################################

# let binding
let pattern = value;

# constants are let const bindings
let const pattern = value;

# statics are let static bindings
let static pattern = value;

# regular and static let's can be mutable, using the mut keyword
let mut static pattern = value;
let mut pattern = value;

################################################################################
# control flow
################################################################################

# if
if (expression) =
else if (expression) =
else =
;;

# match
match (expression) =
    pattern => expression,
    pattern2 => expression,
    pattern3 => 
        multiline_expression
    ;;
;;

# tail recursion optimization is guaranteed if the return statement is of the form
main () =
    return main();
;;
# so no other stuff happens in the return statement apart from calling itself

# loops
# infinite loop
loop =
;;

# break from a loop
loop =
    break;
;;

# continue to next iteration
loop =
    continue;
;;

# break can return a value
loop =
    break 1;
;;

# loops can be named
# then break can exit to that scope
loop: name =
    break(name) 1;
;;

# while loop
while: name (expression) =
;;

# do while loop
do while: name (expression) =
;;

# for each loop
for: name (i in iterable) =
;;

# blocks
# blocks represent scope like all other blocks
block: name =
;;

################################################################################
# classes
################################################################################

# classes are like haskell typeclasses

# normal functions syntax is used, to provide a default body just do a normal function def
# to not use a default body just exlude the equals sign
class name =
    name () =
    ;;

    name2 ();;
;;

# associated types
class name =
    type name;;
;;

# associated constants
class name =
    let const name: Type;
;;

# generics
class name <T> =
;;

# to implement methods on a type you use the instance keyword
# this can only be done on distinct types and not on type aliases
# to assign associated constants you use let const
instance T =
    let const NAME = "Hello World";
    func name () =
    ;;
;;

# to implement a class for a type you also use the instance keyword
instance T of ClassName =
;;

# to implement a class with generics or a type with generics
# use the instance<> syntax
instance<T> A<T> =
;;
```