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
name (a: u8, b: u16) u32 =
;;

# generics
name <A: Eq + Ord> => (a: A) =
;;

# Higher kinded types
# most types have a kind of (*)
# a type that has generics has a kind of (* -> *)
# more generics is more stars (*, * -> *)
# nested kinds are possible ((*, * -> *) -> *)
# the default kind of generics is (*)
name <A: (* -> *), T: Eq> => (input: A<T>) =
;;

# generic packs
# the example makes a tuple of different types
# this is done with the pack bound and the unpack keyword
# what this means is that A cannot be treated as a normal type anymore
# it can only be used in the context of unpack
name <A: pack + Eq> => (input: (unpack A))

# genric packs can specify a minimum and maximum number of types
name <A: pack(min: 2, max: 5)> => (input: (unpack A)) =
;;

# generics can have default values
name <A: Eq = u8> => (input: A) =
;;

# compile time constants can be specified using the let keyword and a type
name <let array_len: usize> => (input: [array_len]u8) =
;;
# or with default value
name <let array_len: usize = 5> => (input: [array_len]u8) =
;;

# kind packs
# if the arity of the kinds is higher or lower than the parameter pack
# there will be a compile error
name <A: (pack(min: 3, max: 5) * -> *), B: pack> => (input: A<unpack B>)

# calling a function
# lets say we have the following function:
name <
    A: (pack * -> *),
    B: pack,
    let c: usize
> => (input: [c]A<unpack B>) =
;;
# to call this function you do the following:
name<A = Either, B = [u8, u16], c = 2>( { Either::Right(200), Either::Left(300) } )

################################################################################
# types
################################################################################

# struct
type name = struct
    field1: u8,
    field2: u8;
;;

# tuple
type name = (u8, u16);;

# sum type
type name = sum
    | Name1 of u8
    | Name2 of u16
    | Name3;
;;

# array
# this is an array of 5 u8's
type name = [5]u8;;
# this is an array of 
```