# Python Style Guid
### Lint

Run `pylint` over your code.


You can get a list of `pylint` warnings by doing:

```shell
pylint --list-msgs
```

To get more information on a particular message, use:

```shell
pylint --help-msg=C6409
```


You can disable specific warnings over all code by addind warning message to *.pylintrc* file
```
[MESSAGES CONTROL]
disable="warning-msg"
```

## Python Style Rules

### 1) Line length
Maximum line length is *80 characters*.

### 2) Parentheses

Use parentheses sparingly.

It is fine, though not required, to use parentheses around tuples. Do not use
them in return statements or conditional statements unless using parentheses for
implied line continuation or to indicate a tuple.

### 3) Indentation

Indent your code blocks with *4 spaces*.

Never use tabs or mix tabs and spaces. In cases of implied line continuation,
you should align wrapped elements either vertically, as per the examples in the
[line length](#s3.2-line-length) section; or using a hanging indent of 4 spaces,
in which case there should be nothing after the open parenthesis or bracket on
the first line.

```python {.good}
Yes:   # Aligned with opening delimiter
       foo = long_function_name(var_one, var_two,
                                var_three, var_four)
       meal = (spam,
               beans)

       # Aligned with opening delimiter in a dictionary
       foo = {
           long_dictionary_key: value1 +
                                value2,
           ...
       }

       # 4-space hanging indent; nothing on first line
       foo = long_function_name(
           var_one, var_two, var_three,
           var_four)
       meal = (
           spam,
           beans)

       # 4-space hanging indent in a dictionary
       foo = {
           long_dictionary_key:
               long_dictionary_value,
           ...
       }
```

```python {.bad}
No:    # Stuff on first line forbidden
       foo = long_function_name(var_one, var_two,
           var_three, var_four)
       meal = (spam,
           beans)

       # 2-space hanging indent forbidden
       foo = long_function_name(
         var_one, var_two, var_three,
         var_four)

       # No hanging indent in a dictionary
       foo = {
           long_dictionary_key:
           long_dictionary_value,
           ...
       }
```
### 4) Blank Lines

Two blank lines between top-level definitions, one blank line between method
definitions.

Two blank lines between top-level definitions, be they function or class
definitions. One blank line between method definitions and between the `class`
line and the first method. Use single blank lines as you judge appropriate
within functions or methods.
### 5) Whitespace

Follow standard typographic rules for the use of spaces around punctuation.

No whitespace inside parentheses, brackets or braces.

```python {.good}
Yes: spam(ham[1], {eggs: 2}, [])
```

```python {.bad}
No:  spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

No whitespace before a comma, semicolon, or colon. Do use whitespace after a
comma, semicolon, or colon except at the end of the line.

```python {.good}
Yes: if x == 4:
         print(x, y)
     x, y = y, x
```

```python {.bad}
No:  if x == 4 :
         print(x , y)
     x , y = y , x
```

No whitespace before the open paren/bracket that starts an argument list,
indexing or slicing.

```python {.good}
Yes: spam(1)
```

```python {.bad}
No:  spam (1)
```


```python {.good}
Yes: dict['key'] = list[index]
```

```python {.bad}
No:  dict ['key'] = list [index]
```

Surround binary operators with a single space on either side for assignment
(`=`), comparisons (`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and
Booleans (`and, or, not`). Use your better judgment for the insertion of spaces
around arithmetic operators but always be consistent about whitespace on either
side of a binary operator.

```python {.good}
Yes: x == 1
```

```python {.bad}
No:  x<1
```

Never use spaces around the '=' sign when passing keyword arguments,
do not use spaces around '=' for default parameter values otherwise.

```python {.good}
Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
```

```python {.bad}
No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
```

Don't use spaces to vertically align tokens on consecutive lines, since it
becomes a maintenance burden (applies to `:`, `#`, `=`, etc.):

```python {.good}
Yes:
  foo = 1000  # comment
  long_name = 2  # comment that should not be aligned

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
```

```python {.bad}
No:
  foo       = 1000  # comment
  long_name = 2     # comment that should not be aligned

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }
```
### 6) Docstrings
#### 6.1) Functions and Methods

A function must have a docstring, unless it meets all of the following criteria:

-   not externally visible
-   very short
-   obvious

A docstring should give enough information to write a call to the function
without reading the function's code. The docstring should be descriptive
(`"""Fetches rows from a Bigtable."""`) rather than imperative
(`"""Fetch rows from a Bigtable."""`). A docstring should describe the
function's calling syntax and its semantics, not its implementation. For tricky
code, comments alongside the code are more appropriate than using docstrings.

A method that overrides a method from a base class may have a simple docstring
sending the reader to its overridden method's docstring, such as
`"""See base class."""`. The rationale is that there is no need to repeat in
many places documentation that is already present in the base method's
docstring. However, if the overriding method's behavior is substantially
different than that of the overridden method or details need to be provided
about it (e.g., documenting additional side-effects), a docstring is required on
the overriding method, with at least those differences.

Certain aspects of a function should be documented in special sections, listed
below. Each section begins with a heading line, which ends with a colon.
Sections should be indented two spaces, except for the heading.

*Args:*
: List each parameter by name. A description should follow the name, and be
: separated by a colon and a space. If the description is too long to fit on a
: single 80-character line, use a hanging indent of 2 or 4 spaces (be
: consistent with the rest of the file).<br/> 
: The description should include required type(s) if the code does not contain
: a corresponding type annotation.<br/>
: If a function accepts `*foo` (variable length argument lists) and/or `**bar`
: (arbitrary keyword arguments), they should be listed as `*foo` and `**bar`.

*Returns:* (or *Yields:* for generators)
: Describe the type and semantics of the return value. If the function only
: returns None, this section is not required. It may also be omitted if the
: docstring starts with Returns (or Yields) (e.g.
: `"""Returns row from Bigtable as a tuple of strings."""`) and the opening
: sentence is sufficient to describe return value.

*Raises:*
: List all exceptions that are relevant to the interface.

```python {.good}
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
```

#### 6.2) Classes

Classes should have a docstring below the class definition describing the class.
If your class has public attributes, they should be documented here in an
Attributes section and follow the same formatting as a function's Args section.

```python {.good}
class SampleClass(object):
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```
#### 6.3) Block and Inline Comments
If you're going to have to explain it at the next code review you should comment it now.
Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line.

```python {.good}
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:  # True if i is 0 or a power of 2.
```

To improve legibility, these comments should be at least 2 spaces away from the
code.

On the other hand, never describe the code. Assume the person reading the code
knows Python (though not what you're trying to do) better than you do.

```python {.bad}
# BAD COMMENT: Now go through the b array and make sure whenever i occurs
# the next element is i+1
```
#### 6.4) TODO Comments

Use `TODO` comments for code that is temporary, a short-term solution, or
good-enough but not perfect.

`TODO`s should include the string `TODO` in all caps, followed by the
name, e-mail address, or other identifier
of the person or issue with the best context about the problem referenced by the
`TODO`, in parentheses. A comment explaining what there is to do is required.
The main purpose is to have a consistent `TODO` format that can be searched to
find out how to get more details upon request. A `TODO` is not a commitment that
the person referenced will fix the problem. Thus when you create a `TODO`, it is almost always your name that is given.

```python {.good}
# TODO(kl@gmail.com): Use a "*" here for string repetition.
# TODO(Zeke) Change this to use relations.
```
### 7) Classes

If a class inherits from no other base classes, explicitly inherit from
`object`. This also applies to nested classes.

```python {.good}
Yes: class SampleClass(object):
         pass


     class OuterClass(object):

         class InnerClass(object):
             pass


     class ChildClass(ParentClass):
         """Explicitly inherits from another class already."""

```

```python {.bad}
No: class SampleClass:
        pass


    class OuterClass:

        class InnerClass:
            pass
```

Inheriting from `object` is needed to make properties work properly in Python 2,
and can protect your code from some potential incompatibility with Python 3. It
also defines special methods that implement the default semantics of objects
including `__new__`, `__init__`, `__delattr__`, `__getattribute__`,
`__setattr__`, `__hash__`, `__repr__`, and `__str__`.

### 8) Strings

Use the `f-strings`, `format` method or the `%` operator for formatting strings, even when
the parameters are all strings. Use your best judgement to decide between `+`, `f-strings`
and `%` (or `format`) though.

```python {.good}
Yes: x = a + b
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}'.format(first, second)
     x = 'name: %s; score: %d' % (name, n)
     x = 'name: {}; score: {}'.format(name, n)
     x = f'name: {name}; score: {n}'  # Python 3.6+
```

```python {.bad}
No: x = '%s%s' % (a, b)  # use + in this case
    x = '{}{}'.format(a, b)  # use + in this case
    x = first + ', ' + second
    x = 'name: ' + name + '; score: ' + str(n)
```

Avoid using the `+` and `+=` operators to accumulate a string within a loop.
Since strings are immutable, this creates unnecessary temporary objects and
results in quadratic rather than linear running time. Instead, add each
substring to a list and `''.join` the list after the loop terminates.

```python {.good}
Yes: items = ['<table>']
     for last_name, first_name in employee_list:
         items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
     items.append('</table>')
     employee_table = ''.join(items)
```

```python {.bad}
No: employee_table = '<table>'
    for last_name, first_name in employee_list:
        employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
    employee_table += '</table>'
```

Use `"` character on a strings. It is okay to use the other quote character on a
string to avoid the need to `\\` escape within the string. `gpylint` enforces
this.

```python {.good}
Yes:
  Python('Why are you hiding your eyes?')
  Gollum("I'm scared of lint errors.")
  Narrator('"Good!" thought a happy Python reviewer.')
```

```python {.bad}
No:
  Python("Why are you hiding your eyes?")
  Gollum('The lint. It burns. It burns us.')
  Gollum("Always the great lint. Watching. Watching.")
```

Prefer `"""` for multi-line strings rather than `'''`. Projects may choose to
use `'''` for all non-docstring multi-line strings if and only if they also use
`'` for regular strings. Docstrings must use `"""` regardless. Note that it is
often cleaner to use implicit line joining since multi-line strings do not flow
with the indentation of the rest of the program:

```python {.good}
  Yes:
  print("This is much nicer.\n"
        "Do it this way.\n")
```

```python {.bad}
  No:
    print("""This is pretty ugly.
Don't do this.
""")
```


### 9) Imports formatting

Imports should be on separate lines.

E.g.:

```python {.good}
Yes: import os
     import sys
```

```python {.bad}
No:  import os, sys
```

Imports are always put at the top of the file, just after any module comments
and docstrings and before module globals and constants. Imports should be
grouped with the order being most generic to least generic:

1.  Python standard library imports. For example:

```python {.good}
    import sys
```

2.  [third-party](https://pypi.python.org/pypi)
    module or package imports. For example:

    
```python {.good}
    import tensorflow as tf
```

3.  Code repository
    sub-package imports. For example:

    
   ```python {.good}
    from otherproject.ai import mind
   ```

4.  application-specific imports that are part of the same
    top level
    sub-package as this file. For example:

    
 ```python {.good}
    from myproject.backend.hgwells import time_machine
```

Within each grouping, imports should be sorted lexicographically, ignoring case,
according to each module's full package path. Code may optionally place a blank
line between import sections.

```python {.good}
import collections
import Queue
import sys

import argcomplete
import BeautifulSoup
import cryptography
import tensorflow as tf

from otherproject.ai import body
from otherproject.ai import mind
from otherproject.ai import soul

from myproject.backend.hgwells import time_machine
from myproject.backend.state_machine import main_loop
```

### 10) Statements

Generally only one statement per line.

However, you may put the result of a test on the same line as the test only if
the entire statement fits on one line. In particular, you can never do so with
`try`/`except` since the `try` and `except` can't both fit on the same line, and
you can only do so with an `if` if there is no `else`.

```python {.good}
Yes:

  if foo: bar(foo)
```

```python {.bad}
No:

  if foo: bar(foo)
  else:   baz(foo)

  try:               bar(foo)
  except ValueError: baz(foo)

  try:
      bar(foo)
  except ValueError: baz(foo)
```


### 11) Naming

`module_name`,
`package_name`,
`ClassName`,
`method_name`,
`ExceptionName`,
`function_name`,
`GLOBAL_CONSTANT_NAME`,
`global_var_name`,
`instance_var_name`,
`function_parameter_name`,
`local_var_name`.

Function names, variable names, and filenames should be descriptive; eschew
abbreviation. In particular, do not use abbreviations that are ambiguous or
unfamiliar to readers outside your project, and do not abbreviate by deleting
letters within a word.

