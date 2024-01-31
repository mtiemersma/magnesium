Type system
===========

The magnesium language provides a lot of high and low level control over types.
The language supports a lot of object oriented features, mixed with concepts
from functional languages. This means higher kinded types and generalized
algabraic data types are supported, but low level things like memory layout and
alignment can also be specified.

User defined types
------------------

Like in haskell, you can define a new algabraic data type using the ``data``
keyword. A type needs a valid identifier as a name and can be one of four
types: empty, sum, product or tuple.

This is the syntax for an empty type:

.. code-block:: magnesium

   data EmptyType;

An empty type is guaranteed to take up no space and is purely a compile time
construct. That being said, it works like every other type, and you don't need
to treat this any different than you would other types.

This is the syntax of sum types:

.. code-block:: magnesium

   data SumType
   {
      | Variant1
      | Variant2(u8, u16)
      | Variant {
         x: u8,
         y: u16
      }
   }

Sum types are descriminated unions, which means that they are safe to use since
you will always know what the current active variant is. As shown above, sum
type variants can have the same types as regular types, excluding sum.

This is the syntax of product types:

.. code-block:: magnesium

   data ProductType
   {
      x: u8,
      y: u16
   }

Product types are like normal structs in other languages.

This is the syntax of tuple types:

.. code-block:: magnesium

   data TupleType(u8, u16);

These tuples are just the same as normal tuples, with the exception that these
are named. Normal tuple types are made like this:

.. code-block:: magnesium

   (u8, u16)

Generics
--------

Generics are a way to have type paramters, where you don't need to know the
actual type but only it's behavior. This can be very general, like only having a
parameter without constraints, but can be narrowed down using class bounds.
Generics have to be used or otherwise hidden using phantom syntax.

Generics can be declared using the generics syntax:

.. code-block:: magnesium

   data Name<phantom A, B: Bound1 + Bound2>
   {
      content: B
   }

You can also have parameter packs, which are like tuples of types. These can be
used to group an arbitrary amount of types, but you can specify constraints such
as a minimum and maximum amount of required types. You can then unpack these
parameter packs to use in types. Syntactically these unpacked packs are like a
comma separated list of the types.

This is the syntax for parameter packs:

.. code-block:: magnesium

   data Name<pack(min: 1, max: 5) A>
   {
      content: (unpack A)
   }

What we also support are const generics, which are constants you pass in the
same way as normal generics. You can use these const generics in other generics,
parameter packs and normal code. Const generics have a type like normal
variables. const generics can also be phantom.

This is the syntax for const generics:

.. code-block:: magnesium

   data Name <phantom const A: u8>;

Bounded types
-------------

Bounded types are like existential quantification in haskell. They create a new
type that cannot be explicitly specified or referenced outside of the type. This
kind of type uses almost the same syntax as generics. Bounded types are declared
using the ``forall`` keyword, like in haskell. Bounded types cannot be phantom,
because there is no way to specify them. So that means they are inferred, which
is not possible if you don't use them.

Bounded type syntax:

.. code-block:: magnesium

   data Name
   forall A: Bound1 + Bound2
   (A, A);

Type classes
------------