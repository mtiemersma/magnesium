# functions

```
func name<T>(a: T): T {};

func name() {
    // long function
};

func name(): u8 = 1; // only the return type
```

lambdas:

```
lambda(x: u8): u8 {1};
```

as closure with capture list:
first argument can be without name, in that case its the default for unspecified
captures

also anything else than move cannot leave the current function

```
let x = 1;
lambda[&] { x }; // x here is of type &usize

lambda[&]; // by reference
lambda[&mut] // by mutable reference

lambda[=] // by move
lambda[=mut] // by mutable move
```

coroutines are resumable functions, currently only stackless coroutines
are supported

```
co func name() {
    yield;
}
```
# types

```
type Name<A, B: Bound, pack(min = 1, max = 5) C, D: (* -> * -> *), const ARRAY_SIZE: u8>
forall a, b: Bound + Bound2.
{
    name_a: A,
    name_b: B,
    tuple: {a, b},
    packed: {unpack C},
    hkt: D<A, B>,
    sum: forall c, d. {
        VariantOne of c,
        VariantTwo of d,
        MarkerVariantOne,
        MarkerVariantTwo
    },
    array: [ARRAY_SIZE]u8
}

type Name<A, B> {
    GADTVariantOne when <u16, u32> of {A, B},
    GADTVariantTwo when <u32, u64> of {A, B},
}
```

# type classes
```
class Name <U>
forall a.
{
    func function_one;
    func function_two(u8, u16): u32;
    func function_three<A>: A;

    type Associated_T<T>: Bound;

    const ASSOCIATED_CONSTANT: Self.Associated_T;
}
```

implement with ``impl``

```
impl<T> Class<T> for Type {}

impl Class for T; // marker class

impl T {}; // base implementation
```

you can implement classes with items that have the same name. To specify which
is used, use absolute module syntax

# variables

```
const name = 0;

static name = 0;

static mut name = 0;
```

```
let immutable = 0;

let mut mutable = 0;
```

# memory

to allocate use `new` keyword
WARNING: anything else than box variants need manual deallocation
```
new 1; // Box<usize>
new ref 1; // RefBox<usize>
new atomic 1; // AtomicBox<usize>

new reference 1; // &usize
new reference mut 1; // &mut usize

new raw 1; // *usize
new raw mut 1; // *mut usize
```

you can also get a

# builtin types

```
Box<T> // box type
RefCountBox<T> // reference counted box
AtomicBox<T> // atomic reference counted box

&T // reference
&mut T // mutable reference

*T // raw pointer
*mut T // mutable raw pointer

[]T // slice
[]mut T // mutable slice

[N]T // array of N items
[N]mut T // mutable array of N items

Uninit<T> // possible unitialized T, acts like normal T, except no method calls

u8, u16, u32, u64, u128 // unsigned integers
i8, i16, i32, i64, i128 // signed integers

// IEEE 754 floating point numbers
f16, f32, f64, f128, f256 // binary floating point numbers
```

# builtin type classes

```
Tuple, method len(): usize
```

# control flow

if expression

```
if expr {} else if {} else {}
```

match expression

```
match expr {
    1 => {},
    2 | 3 => {},
    _ => 0
}
```

for loop

```
for x in iter {}
```

while loop

```
while expr {}

do while expr {}
```

`continue` skips to next iteration

`break` exits current loop and returns optional value, default is `()`

matching in loops and if statements

```
if let pattern = expr {}

while let pattern = expr {}
```

# operators

`-x` unary negation

`x + y` adding
`x - y` subtraction
`x * y` multiplication
`x / y` division
`x % y` modulo

`x[]` subscript
`x.*` dereference
`&x` take reference
`&mut` take mutable reference

`x && y` logical AND
`x || y` logical OR
`!x` logical NOT

`~x` bitwise not
`x ^ y` bitwise xor
`x & y` bitwise and
`x | y` bitwise or
`x << y` bitwise left shift
`x >> y` bitwise right shift

# module system

import

```
import @"file".item;

import @libname.item;

import item.subitem;

import item.*;

import item.{
    subitem1,
    subitem2.subitem3
};

import item as newname;
```

to make an item available to be imported, use pub keyword
```
pub func name() {}
```

this keyword can be modified using a few keywords

```
pub(pkg) // only in the current package
pub(mod) // only in the current module
```

# build tools
