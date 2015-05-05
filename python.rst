======
Python
======

Contents:
---------

+ `Summary`_
+ `Package Structure`_
+ `Naming Conventions`_
+ `Code Sections`_
+ `Classes`_
+ `Docstrings`_

Summary
-------

**General Rule:** Follow PEP8_.

Package Structure
-----------------

<add me>

Naming Conventions
------------------

+ Class names are CamelCase
+ Module-level constants are UPPERCASE with underscores for
  readability (MAX_CONSTANT)
+ methods and functions are lowercase_with_underscores

Code Sections
-------------

+ Sections within a function or method should be denoted by::

  ### Section Name ####################################################

  - the last hash mark should fill column 77.
  - additional comments can follow this section header

+ collections of similar functions should be denoted by::

    ### #--------------------------------------------------------------------
    ### Group or Section
    ### #--------------------------------------------------------------------
    
  - This is also how various class setions are denoted.

Classes
-------

+ Class Names are CamelCase
+ ``__init__`` is the first method in any class
+ The class order is as follows:

  1.  ``__magic__`` methods
  2.  ``__mangled`` methods
  3.  ``_private`` methods
  4.  ``public`` methods

+ Event handlers

  + begin with ``on_`` for public handlers or ``_on_`` for
    private handlers.

  + are listed at the end of their respective section

+ Class sections are broken up by the following, with a single enter before
  and after::

    ### #--------------------------------------------------------------------
    ### Class Section
    ### #--------------------------------------------------------------------

  - Note that there is no space after the hash on the pre- and post-lines

+ Each method needs some kind of docstring

Docstrings
----------

Whenever possible, try to follow the numpydoc_ convention. Although, the short summary
should start on line two::

  def my_func(a):
      """
      This is the short summary.
      """
      pass









.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _numpydoc: https://github.com/numpy/numpy/blob/master/doc/HOWTO_DOCUMENT.rst.txt
