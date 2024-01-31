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

    func name(arg1: u8, arg2: u16) u32
    {
        # function body
    }

Generics and such
-----------------

Generics, bounded types, and const generics are explained in the
:doc:`types <types>` section of the reference.

Lambdas and closures
--------------------

Lambdas are almost equivalent to normal function declarations, except that when
they are declared, you don't put an identifier behind the ``func`` keyword.

Closures however, are another matter entirely. Closures have to have a so called
capture list. This is similar to how CPP handles closures. You can capture in a
few different ways. To give a default mode of capture, the first argument can be
given without a variable to capture.

- by move
- by reference, mutable or not
- by raw pointer, mutable or not
- by smart pointer
    - box
    - shared_box
    - atomic_box

There are some restrictions to capturing variables. You cannot capture by
reference if the closure will leave the scope it is defined in, and anything
other than capturing by reference or pointer will move the values. By default
the 

This is the syntax for capture lists, where ``a`` and ``b`` are variables in the
scope of the function they are defined in.

.. code-block:: magnesium

    func[=] {} # move

    func[&] {} # reference
    func[&mut] {} # mutable reference

    func[*] {} # raw pointer
    func[*mut] {} # mutable raw pointer

    func[box] {} # box
    func[shared_box] {} # shared box
    func[atomic_box] {} # atomic box

    func[=a, box b] {}