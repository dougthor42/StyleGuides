======
Python
======

Contents:
---------

+ `Summary`_
+ `Package Structure`_
+ `Naming Conventions`_
+ `Code Sections`_

  + `Imports`_
  
+ `Classes`_
+ `Docstrings`_

Summary
-------

**General Rule:** Follow PEP8_.

Package Structure
-----------------

::

  PackageName
  │   .gitignore
  │   .travis.yml
  │   appveyor.yml
  │   build_exe.bat
  │   build_executables.py
  │   dev-requirements.txt
  │   LICENSE
  │   README.rst
  │   setup.py
  │
  ├───appveyor                       (scripts for Appveyor CI)
  │       get-7zip.ps1
  │       install.ps1
  │       run_with_env.cmd
  │
  ├───build                          (built executables)
  ├───build_reqs                     (wheels required by CI services)
  ├───dist                           (source distribution files)
  ├───doc                            (documentation)
  ├───img                            (supporting images)
  ├───log                            (log files)
  └───packagename
      │   __init__.py
      │   main_module.py
      │   supporting_module_1.py
      │   supporting_module_2.py
      │
      └───tests
          │    __init__.py
          │    test_main_module.py
          │    test_supporting_module_1.py
          │    test_supporting_module_2.py
          │
          └────data                 (data files used for unit tests)

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

    # ---------------------------------------------------------------------------
    ### Section Name
    # ---------------------------------------------------------------------------
    
  - This is also how various class setions are denoted.

Imports
=======

+ Imports should be organized into three sections: Standard Library, Third-Party, and then within-Package.
+ Each section should be in alphabetical order
+ When ``from x import y`` is used, it it placed at the end of the section.

Example::

  # ---------------------------------------------------------------------------
  ### Imports
  # ---------------------------------------------------------------------------
  # Standard Library
  import configparser
  import os
  import os.path as osp

  # Third-Party
  import numpy as np
  import wafer_map.wm_core as wm_core
  import wx
  import wx.lib.plot as wxplot
  from wx.lib.floatcanvas import FloatCanvas

  # Package / Application
  (See below)

For various reasons, I've found that the within-Package imports must be formatted like so::

  # Package
  try:
      # Imports used by UnitTests
      from . import supporting_module_1
      from . import supporting_module_2
      from . import (__project_name__,
                     __version__,
                     __released__,
                     )
      #logging.debug("Imports for UnitTests")
  except SystemError:
      try:
          # Imports used by Spyder
          import supporting_module_1
          import supporting_module_2
          from __init__ import (__project_name__,
                                __version__,
                                __released__,
                                )
          #logging.debug("Imports for Spyder IDE")
      except ImportError:
          # Imports used by cx_freeze
          from packagename import supporting_module_1
          from packagename import supporting_module_2
          from packagename import (__project_name__,
                                   __version__,
                                   __released__,
                                   )
          #logging.debug("Imports for Executable")

Classes
-------

+ Class Names are CamelCase
+ ``__init__`` is the first method in any class
+ The class order is as follows:

  1.  ``__magic__`` methods
  2.  ``__mangled`` methods
  3.  ``_private`` methods
  4.  ``public`` methods
  5.  ``_on_private`` event handlers
  6.  ``on_public`` event handlers

+ Event handlers

  + begin with ``on_`` for public handlers or ``_on_`` for
    private handlers.

+ Class sections are broken up by the following, with a single enter before
  and after::

    # -----------------------------------------------------------------------
    ### Class Section
    # -----------------------------------------------------------------------

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
