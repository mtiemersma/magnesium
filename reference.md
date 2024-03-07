# variables

```
const name = val;

static name = val;

static mut name = val;

let name = val;

let mut name = val;
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
impl T {
    const name = 0;

    func name() {}
}
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
```

# builtins

types:
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
impl Class for T {}
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