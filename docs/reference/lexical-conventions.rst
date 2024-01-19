Lexical conventions
===================

Source character set
--------------------

Currently the only allowed character set for magnesium source files is utf8,
which, at the time of writing, is the industry standard way of encoding plain
text. I tried to keep the required characters to within the ASCII range, but
you can use any valid unicode sequence for things like identifiers, as long as
they don't conflict with rules specified by this document. It is however advised
to keep identifiers and such constrained to the ascii range and english, as this
makes the software you write as portable as possible and it will be understood
well by most programmers, but this is not a requirement.

Comments
--------

Comments in this language are started by the ``#`` character. This is similar to
bash and python in that regard.

There are two types of doc comments. One for describing items inside files, and
one for describing the files themselves. Doc comments describing items are
started with a ``##`` and put directly above the item they describe. Doc
comments describing files themselves are started with ``#!`` and can only be
placed at the top of the file they are documenting.

Doc comments are styled with markdown.

Example:

.. code-block:: magnesium

    #! file doc comment
    
    ## doc comment
    
    # regular comment

Identifiers
-----------

As stated before, identifiers can be made up of any valid utf8 sequence. There
are some exceptions to this rule however. Identifiers cannot be only keywords,
but they can include them. For example ``let`` cannot be an identifier, because
it is a keyword, but ``letter`` is valid. An identifier can also not be a number
literal, but like with keywords, they can be a part of an identifier. So ``0``
is not a valid identifier but ``0_one_two`` is. It is however strongly
discouraged to to use numbers in identifiers. Identifiers can also not include
whitespace.

Keywords
--------

Keywords are special reserved names and directives reserved by the compiler for
internal use. These cannot be used in source code for other purposes than their
original meaning.

Here is a list of all currently reserved keywords:

Memory related:
    - ``new``, allocates memory using the provided allocator
    - ``delete``, deallocates memory using the provided memory allocator

Variable related:
    - ``partial``, makes an object partially constructed
    - ``let``, constructs a new variable using a pattern
    - ``mut``, used as a modifier with many keywords, makes something mutable

Function related:
    - ````

Type related:
    - ``instance``, adds members and constants to types
    - ``type``, adds a new type