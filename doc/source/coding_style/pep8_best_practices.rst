PEP 8 Best Practices
====================
This topic summarizes key points from `PEP 8`_ and how
they apply to PyAnsys libraries. The goal is for PyAnsys libraries to
be consistent in style and formatting with the `big three`
data science libraries: `NumPy`_, `SciPy`_, and `pandas`_.


Imports
~~~~~~~
Imports should always be placed at the top of the file, just after any
module comments and docstrings and before module globals and
constants.  This reduces the likelihood of an `ImportError`_ that
might only be discovered during runtime.

Instead of:

.. code:: python

   def compute_logbase8(x):
       import math
       return math.log(8, x)

Use:

.. code:: python

    import math

    def compute_logbase8(x):
        return math.log(8, x)


For better readability, group imports in this order:

#. Standard library imports
#. Related third-party imports
#. Local application- or library-specific imports

Instead of:

.. code:: python

   import sys
   import subprocess
   from mypackage import mymodule
   import math

   def compute_logbase8(x):
      return math.log(8, x)


Use:

.. code:: python

   import sys
   import subprocess
   import math
   from mypackage import mymodule

   def compute_logbase8(x):
       return math.log(8, x)


You should place imports in separate lines unless they are
modules from the same package.

Instead of:

.. code:: python

   import sys, math
   from my_package import my_module
   from my_package import my_other_module

   def compute_logbase8(x):
       return math.log(8, x)

Use:

.. code:: python

   import sys
   import math
   from my_package import my_module, my_other_module

   def compute_logbase8(x):
       return math.log(8, x)


You should avoid using wild cards in imports because doing so
can make it difficult to detect undefined names.  For more information,
see `Python Anti-Patterns: using wildcard imports`_.

Instead of:

.. code:: python

    from my_package.mymodule import *

Use:

.. code:: python

    from my_package.my_module import myclass


Indentation and Line Breaks
---------------------------
Proper and consistent indentation is important to producing
easy-to-read and maintainable code. In Python, use four spaces per
indentation level and avoid tabs. 

Indentation should be used to emphasize:

 - Body of a control statement, such as a loop or a select statement
 - Body of a conditional statement
 - New scope block

.. code:: python

   class MyFirstClass:
       """MyFirstClass docstring"""

   class MySecondClass:
       """MySecondClass docstring"""

   def top_level_function():
       """Top level function docstring"""
       return

For improved readability, add blank lines or wrapping lines. Two
blank lines should be added before and after all function and class
definitions.

Inside a class, use a single line before any method definition.

.. code:: python

   class MyClass:
       """MyClass docstring"""

   def first_method(self):
       """First method docstring"""
       return

   def second_method(self):
       """Second method docstring"""
       return

To make it clear when a 'paragraph' of code is complete and a new section
is starting, use a blank line to separate logical sections.

Instead of:

.. code::

   if x < y:

       STATEMENTS_A

   else:

       if x > y:

           STATEMENTS_B

       else:

           STATEMENTS_C

   if x > 0 and x < 10:

       print("x is a positive single digit.")

Use:

.. code::

   if x < y:
       STATEMENTS_A
   else:
       if x > y:
           STATEMENTS_B
       else:
           STATEMENTS_C

   if x > 0 and x < 10:
       print("x is a positive single digit.")
   elif x < 0:
       print("x is less than zero.")


Maximum Line Length
-------------------
For source code lines, best practice is to keep the length at or below
100 characters. For docstrings and comments, best practice is to keep
the length at or below 72 characters.

Lines longer than these recommended limits might not display properly
on some terminals and tools or might be difficult to follow. For example,
this line is difficult to follow:

.. code:: python

   employee_hours = [schedule.earliest_hour for employee in self.public_employees for schedule in employee.schedules]

The line can be rewritten as:

.. code:: python

   employee_hours = [schedule.earliest_hour for employee in
                     self.public_employees for schedule in employee.schedules]

Alternatively, instead of writing a list comprehension, you can use a
classic loop.


Naming Conventions
------------------
To achieve readable and maintainable code, use concise and descriptive names for classes,
methods, functions, and constants. Regardless of the programming language, you must follow these
global rules to determine the correct names:

#. Choose descriptive and unambiguous names.
#. Make meaningful distinctions.
#. Use pronounceable names.
#. Use searchable names.
#. Replace magic numbers with named constants.
#. Avoid encodings. Do not append prefixes or type information.


Names to Avoid
~~~~~~~~~~~~~~
Do not use the characters ``'l'``, ``'O'`` , or ``'I'`` as
single-character variable names. In some fonts, these characters are
indistinguishable from the numerals one and zero.


Package and Module Naming Conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use a short, lowercase word or words for module names. Separate words
with underscores to improve readability. For example, use ``module.py``
or ``my_module.py``.

For a package name, use a short, lowercase word or words. Avoid
underscores as these must be represented as dashes when installing
from PyPi.

.. code::

   pip install package


Class Naming Conventions
~~~~~~~~~~~~~~~~~~~~~~~~
Use `camel case`_ when naming classes. Do not separate words
with underscores. 

.. code:: python

   class MyClass():
       """Docstring for MyClass"""
       pass


Function and Method Naming Conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use a lowercase word or words for Python functions or methods. Separate
words with underscores to improve readability. 

.. code:: python

   class MyClass():
       """Docstring for MyClass"""

       def __init__(self, value):
           """Constructor.

           Methods with double underscores on either side are called
           "dunder" methods and are special Python methods.

           """
           self._value = value

       def __private_method(self):
           """This method can only be called from ``MyClass``."""
           self._value = 0

       def _protected_method(self):
           """This method should only be called from ``MyClass``.

           Protected methods can be called from inherited classes,
           unlike private methods, which names are 'mangled' to avoid
           these methods from being called from inherited classes.

           """
           # note how we can call private methods here
           self.__private_method()

       def public_method(self):
           """This method can be called external to this class."""
           self._value += 2


Variable Naming Conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use a lowercase single letter, word, or words when naming
variables. Separate words with underscores to improve readability.

.. code:: python

    my_variable = 5


Constants are variables that are set at the module level and are used
by one or more methods within that module. Use an uppercase word or
words for constants. Separate words with underscores to improve
readability.

.. code:: python

    PI = 3.141592653589793
    CONSTANT = 4
    MY_CONSTANT = 8
    MY_OTHER_CONSTANT = 1000


Comments
~~~~~~~~
Because a PyAnsys library generally involves multiple physics domains,
users reading its source code do not have the same background as
the developers who wrote it. This is why it is important for a library
to have well commented and documented source code. Comments that
contradict the code are worse than no comments. Always make a priority
of keeping comments up to date with the code.

Comments should be complete sentences. The first word should be
capitalized, unless it is an identifier that begins with a lowercase
letter.

Here are general guidelines for writing comments:

#. Always try to explain yourself in code by making it
   self-documenting with clear variable names.
#. Don't be redundant.
#. Don't add obvious noise.
#. Don't use closing brace comments.
#. Don't comment out code that is unused. Remove it.
#. Use explanations of intent.
#. Clarify the code.
#. Warn of consequences.

Obvious portions of the source code should not be commented. 
For example, the following comment is not needed:

.. code:: python

   # increment the counter
   i += 1

However, an important portion of the behavior that is not self-apparent
should include a note from the developer writing it. Otherwise,
future developers may remove what they see as unnecessary. 

.. code:: python

   # Be sure to reset the object's cache prior to exporting. Otherwise,
   # some portions of the database in memory will not be written.
   obj.update_cache()
   obj.write(filename)


Inline Comments
~~~~~~~~~~~~~~~
Use inline comments sparingly. An inline comment is a comment on the
same line as a statement.

Inline comments should be separated by two spaces from the statement. 

.. code:: python

    x = 5  # This is an inline comment

Inline comments that state the obvious are distracting and should be
avoided:

.. code:: python

    x = x + 1  # Increment x


Focus on writing self-documenting code and using short but
descriptive variable names.  

Instead of:

.. code:: python

   x = 'John Smith'  # Student Name

Use:

.. code:: python

    user_name = 'John Smith'


Docstring Conventions
~~~~~~~~~~~~~~~~~~~~~
A docstring is a string literal that occurs as the first statement in
a module, function, class, or method definition. A docstring becomes
the doc special attribute of the object.

Write docstrings for all public modules, functions, classes, and
methods. Docstrings are not necessary for private methods, but such
methods should have comments that describe what they do.

To create a docstring, surround the comments with three double quotes
on either side.

For a one-line docstring, keep both the starting and ending ``"""`` on the
same line: 

.. code:: python

   """This is a docstring.""".  

For a multi-line docstring, put the ending ``"""`` on a line by itself.

`PyAEDT`_ follows the `numpydoc`_ docstring style, which is used by `numpy`_
`scipy`_, `pandas`_, and a variety of other Python open source projects.  For
more information on docstrings for PyAnsys libraries, see
:ref:`API Documentation Style`.


Programming Recommendations
~~~~~~~~~~~~~~~~~~~~~~~~~~~
The following sections provide some `PEP 8`_ suggestions for removing ambiguity
and preserving consistency. They address some common pitfalls when writing
Python code.


Booleans and Comparisons
------------------------
Don't compare Boolean values to ``True`` or ``False`` using the
equivalence operator.

Instead of:

.. code:: python

   if my_bool == True:
       return result

Use:

.. code:: python

   if my_bool:
       return result

Knowing that empty sequences are evaluated to ``False``, don't compare the
length of these objects but rather consider how they would evaluate
by using ``bool(<object>)``.

Instead of:

.. code:: python

   my_list = []
   if not len(my_list):
       raise ValueError('List is empty')

Use:

.. code:: python

    my_list = []
    if not my_list:
       raise ValueError('List is empty')

In ``if`` statements, use ``is not`` rather than ``not ...``. 

Instead of:

.. code:: python

    if not x is None:
        return x

Use:

.. code:: python

   if x is not None:
       return 'x exists!'

Also, avoid ``if x:`` when you mean ``if x is not None:``.  This is
especially important when parsing arguments.


Handling Strings
----------------
Use ``.startswith()`` and ``.endswith()`` instead of slicing.

Instead of:

.. code:: python

   if word[:3] == 'cat':
       print('The word starts with "cat"')

   if file_name[-3:] == 'jpg':
       print('The file is a JPEG')

Use:

.. code:: python

   if word.startswith('cat'):
       print('The word starts with "cat"')

   if file_name.endswith('jpg'):
       print('The file is a JPEG')


Reading the Windows Registry
----------------------------
Never read the Windows registry or write to it because this is dangerous and 
makes it difficult to deploy libraries on different environments or operating
systems.

Bad practice - Example 1

.. code:: python

   self.sDesktopinstallDirectory = Registry.GetValue("HKEY_LOCAL_MACHINE\Software\Ansoft\ElectronicsDesktop\{}\Desktop".format(self.sDesktopVersion), "InstallationDirectory", '')

Bad practice - Example 2

.. code:: python

    EMInstall = (string)Registry.GetValue(string.Format(@"HKEY_LOCAL_MACHINE\SOFTWARE\Ansoft\ElectronicsDesktop{0}\Desktop", AnsysEmInstall.DesktopVersion), "InstallationDirectory", null);


Duplicated Code
---------------
Follow the DRY principle, which states that "Every piece of knowledge
must have a single, unambiguous, authoritative representation within a
system."  Attempt to follow this principle unless it overly complicates
the code. For instance, the following example converts Fahrenheit to kelvin
twice, which now requires the developer to maintain two separate lines
that do the same thing.

.. code:: python

   temp = 55
   new_temp = ((temp - 32) * (5 / 9)) + 273.15

   temp2 = 46
   new_temp_k = ((temp2 - 32) * (5 / 9)) + 273.15

Instead, write a simple method that converts Fahrenheit to kelvin:

.. code:: python

   def fahr_to_kelvin(fahr)
       """Convert temperature in Fahrenheit to kelvin.

       Parameters:
       -----------
       fahr: int or float
           Temperature in Fahrenheit.

       Returns:
       -----------
       kelvin : float
          Temperature in kelvin.
       """
       return ((fahr - 32) * (5 / 9)) + 273.15

Now, you can execute and get the same output with:

.. code:: python

   new_temp = fahr_to_kelvin(55)
   new_temp_k = fahr_to_kelvin(46)

This is a trivial example, but the approach can be applied for a
variety of both simple and complex algorithms and workflows. Another
advantage of this approach is that you can implement unit testing
for this method.

.. code:: python

   import numpy as np

   def test_fahr_to_kelvin():
       assert np.isclose(12.7778, fahr_to_kelvin(55))

Now, not only do you have one line of code to verify, but you can also
use a testing framework such as ``pytest`` to test that the method is
correct.


Nested Blocks
-------------
Avoid deeply nested block structures (such as conditional blocks and loops)
within one single code block. 

.. code:: python

   def validate_something(self, a, b, c):
       if a > b:
           if a*2 > b:
               if a*3 < b:
                   raise ValueError
           else:
               for i in range(10):
                   c += self.validate_something_else(a, b, c)
                   if c > b:
                       raise ValueError
                   else:
                       d = self.foo(b, c)
                       # recursive
                       e = self.validate_something(a, b, d)


Aside from the lack of comments, this complex method
is difficult to debug and validate with unit testing. It would
be far better to implement more validation methods and join conditional
blocks.

For a conditional block, the maximum depth recommended is four. If you
think you need more for the algorithm, create small functions that are
reusable and unit-testable.


Loops
-----
While there is nothing inherently wrong with nested loops, to avoid
certain pitfalls, steer clear of having loops with more than two levels. In
some cases, you can rely on coding mechanisms like list comprehensions 
to circumvent nested loops. 

Instead of:

.. code::

   >>> squares = []
   >>> for i in range(10):
   ...    squares.append(i * i)
   >>> squares
   [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


Implement a list comprehension with:

.. code::

   >>> squares = [i*i for i in range(10)]
   >>> squares
   [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


If the loop is too complicated for creating a list comprehension,
consider creating small functions and calling these instead. For
example, extract all consonants in a sentence:

.. code:: python

   >>> sentence = 'This is a sample sentence.'
   >>> vowels = 'aeiou'
   >>> consonants = []
   >>> for letter in sentence:
   ...     if letter.isalpha() and letter.lower() not in vowels:
   ...         consonants.append(letter)
   >>> consonants
   ['T', 'h', 's', 's', 's', 'm', 'p', 'l', 's', 'n', 't', 'n', 'c']


This is better implemented by creating a simple method to return if a
letter is a consonant:

   >>> def is_consonant(letter):
   ...     """Return ``True`` when a letter is a consonant."""
   ...     vowels = 'aeiou'
   ...     return letter.isalpha() and letter.lower() not in vowels
   ...
   >>> sentence = 'This is a sample sentence.'
   >>> consonants = [letter for letter in sentence if is_consonant(letter)]
   >>> consonants
   ['T', 'h', 's', 's', 's', 'm', 'p', 'l', 's', 'n', 't', 'n', 'c']

The second approach is more readable and better documented. Additionally,
you could implement a unit test for ``is_consonant``.


Security Considerations
~~~~~~~~~~~~~~~~~~~~~~~

Security, an ongoing process involving people and practices, ensures application confidentiality, integrity, and availability [#]_.
Any library should be secure and implement good practices that avoid or mitigate possible security risks.
This is especially relevant in libraries that request user input (such as web services).
Because security is a broad topic, we recommend you review this useful Python-specific resource:

* `10 Unknown Security Pitfalls for Python`_ - By Dennis Brinkrolf - Sonar source blog


.. LINKS AND REFERENCES
.. include:: ../links.rst
.. [#] Wikipedia - Software development security https://en.wikipedia.org/wiki/Software_development_security
.. _10 Unknown Security Pitfalls for Python: https://blog.sonarsource.com/10-unknown-security-pitfalls-for-python
.. _camel case: https://en.wikipedia.org/wiki/Camel_case
.. _ImportError: https://docs.python.org/3/library/exceptions.html#ImportError
.. _Python Anti-Patterns\: using wildcard imports: https://docs.quantifiedcode.com/python-anti-patterns/maintainability/from_module_import_all_used.html
