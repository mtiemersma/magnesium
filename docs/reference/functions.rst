Functions
=========

Functions are one of the most important parts of the language. Functions are
regions of code that can be reused. Functions can be named or anonymous. There
are two types of anonymous functions. There are lambdas, which are just like
normal functions, and you can have closures. Closures can capture their
environment, but this will be explained later.

Normal functions
----------------

Functions are declared using the ``func`` keyword and named usign an identifier.
functions can accept arguments, and return a value. There is no requirement in
either, but a function will implictly return ``()``, also called unit, if no
return type is specified.

This is function declaration syntax:

.. code-block:: magnesium

    func name(arg1: u8, arg2: u16) u32 {
        # function body
    }

Generics and such
-----------------

Generics, bounded types, and const generics are explained in the
:doc:`types <types>` section of the reference.