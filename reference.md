# variables

```
const name = val;

static name = val;

static mut name = val;

let name = val;

let mut name = val;
```

```
let name: T = val;
```
# types

```
type Name = T;

type alias Name = T;

type Name = struct {
    field1: T,
    field2: T,
};

type Name = union {
    Name1,
    Name2(T),
    Name3 { x, y: i32 }
}

type Name = (T, T2, T3, ...)
```

```
inst T {
    const name = 0;

    func name() {}
}
```

keyword `Self` refers to current type

keyword `self` refers to current object

an associated function can take self or a variant of self as arg
short forms are supported for ptrs and plain objects but not boxes those only have the long form
same with rc's and arc's
```
format = short form | long form

self | self: Self

*self | self: *Self
*mut self | self: *mut Self
```

# functions

```
func name(x: T): T {}

func name() {
    return;
}

func name(): T {
    return expr;
}

func name(x, y: T) {}
```

# lambdas

```
let name = func(arg1: OptType, arg2): OptReturnT => expr;

let min_syntax = func(arg) => expr;
```

# builtins

```
u8, u16, u32, u64, u128, usize
i8, i16, i32, i64, i128, isize

f32, f64

*T, *mut T

*?T, *?mut T

[*]T

[*]? T

[N]T

[]T

[]? T

Uninit<T>

func(T, U, ...): A

Box<T>
BoxMut<T>

RcBox<T>
RcMutBox<T>

ArcBox<T>
ArcMutBox<T>
```

# control flow

```
if expr {}

if expr {} else {}

if expr {} else if expr {} else {}
```

```
match expr {
    1 => expr,
    2 | 3 => expr,
    a @ 4 => expr,
    5 if expr => expr
}
```

```
for expr {}

for expr in iter {}

for {}

for {
    continue;
}

for {
    break;
}

for {
    break expr;
}
```

# operators

```
x[i]
x[..]
x[begin..]
x[..end]
x[begin..end]
x.y
x?

*x
&x
&mut x
!x
~x

x + y
x - y
x * y
x / y
x % y

x == y
x != y
x && y
x || y

x ^ y
x | y
x & y
x << y
x >> y
```

# type classes

```
class Name {
    const name: T;

    const name: isize = 0;

    type Name: Bound;

    type Name: Bound = Default;

    func name(x: T): T;

    func name() {}
}
```

```
inst T of Class {}
```

# generics

```
type Name<T> = T;

func name<T>(x: T) {}

class Name<T> {
    const name: T;
}

type Name<T: ClassBound> = T;

type HKT<T: (* -> *), U> = T<U>;

type ConstGeneric<const N: usize, T> = [N]T;

type Packed<pack(min: 1, max: 5) T> = (unpack T)
```

# GADT's

```
type Name<A, B> = union gadt {
    Name1<u8, u8>(B),
    Name2<u16, u16>,
    Name3<u32, u32> {
        field: A
    }
};
```

# module system

```
pub type Name = T; // pub = pub(all)

pub(all)

pub(pkg)

pub(mod)
```

```
import @"file".item;

import @libname.item;

import @libname.module;
import module.item;

import @lib.item as rename;

pub import item;
pub import item as reexport;
```

# memory

new expression
```
new 1; // Box<usize>
new mut 1; // BoxMut<usize>

new rc 1; // RcBox<usize>
new mut rc 1; // RcMutBox<usize>

new arc 1; // ArcBox<usize>
new mut 1; // ArcMutBox<usize>

new ptr 1; // *usize
new mut ptr; // *mut usize
```

new with lambda initialization
```
new lambda func(arg: Uninit<T>): Box<T> => expr;

new lambda mut func(arg: Uninit<T>): BoxMut<T> => expr;
```

delete expression
```
delete ptr;
```

# macros

function style
```
macro func name(arg1: untyped, arg2: u8): untyped {
}
```

attr style, required arg1: untyped, return untyped
arg1: item being applied to
return: item
```
macro attr name(in: untyped): untyped {
}
```

calling macros:
```
func_style_macro$()

$attr_macro()
// item
```
