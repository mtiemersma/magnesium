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

   data SumType {
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

   data ProductType {
      x: u8,
      y: u16
   }

Product types are like normal structs in other languages.

This is the syntax of tuple types:

.. code-block:: magnesium

   data TupleType()