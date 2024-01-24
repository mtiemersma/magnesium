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
keyword. A type needs a valid identifier as a name and can be one of three
types: empty, sum or product.

This is the syntax for an empty type:

.. code-block:: magnesium

   data TypeName;

An empty type is mostly useful for 