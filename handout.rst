===================
Testing Python
===================

.. class:: right big

  | *Matt Harrison*
  | matthewharrison@gmail.com
  | http://panela.blog-city.com/

.. class:: small

   ©2009-2010, licensed under a `Creative Commons
   Attribution/Share-Alike (BY-SA) license
   <http://creativecommons.org/licenses/by-sa/3.0/>`__.

Doctest
=========

Here is some details about the doctest module.  Taken from the doctest
docs.  (http://docs.python.org/lib/module-doctest.html)

    >>> # comments are ignored
    >>> foo = "bar"
    >>> foo  #implicit print
    'bar'
    >>> if foo == "baz":
    ...   print "baz"
    ... else:
    ...   print foo
    ...
    bar

Whitespace
-----------

Caveats.  Can't print whitespace directly use <BLANKLINE> instead

    >>> print ""
    <BLANKLINE>

Raw text
---------

Backslashes.  Use raw docstrings (this one is) or escape them

    >>> line = "foo\n"  # use \\n if not raw
    >>> print line
    foo
    <BLANKLINE>

Starting column
---------------

Starting column is irrelevant.  Just (try to) be consistent

>>> 2 + 2
4

Exceptions
-----------

Exceptions.  Expected output for an exception must start with a
traceback header.

    >>> [1, 2, 3].remove(42)
    Traceback (most recent call last):
      File "<stdin>", line 1, in ?
    ValueError: list.remove(x): x not in list

Ellipsis
---------

Traceback stack can also be replaced by ellipsis "..."

    >>> [1, 2, 3].remove(42)
    Traceback (most recent call last):
      ...
    ValueError: list.remove(x): x not in list

Whitespace
-----------

Various options and directives.  Note the "#doctest:"

    >>> print range(20) #doctest: +NORMALIZE_WHITESPACE
    [0,   1,  2,  3,  4,  5,  6,  7,  8,  9,
    10,  11, 12, 13, 14, 15, 16, 17, 18, 19]


    >>> print range(20) # doctest: +ELLIPSIS, +NORMALIZE_WHITESPACE
    [0,    1, ...,   18,    19]

    >>> (1, 2)[3] = 'moo' #doctest: +IGNORE_EXCEPTION_DETAIL
    Traceback (most recent call last):
      File "<stdin>", line 1, in ?
    TypeError: object doesn't support item assignment

Dictionary order
-----------------

Dealing with dicts.

    >>> foo = dict(a=1, b="hello", c="bye")
    >>> foo # this might fail
    {'a': 1, 'c': 'bye', 'b': 'hello'}

Workaround is to sort the keys

    >>> items = foo.items()
    >>> items.sort()
    >>> items
    [('a', 1), ('b', 'hello'), ('c', 'bye')]

Addresses
----------

Dealing with addresses 

    >>> class C: pass
    >>> c = C()
    >>> c # will most likely fail
    <__main__.C instance at 0xb7a210ec>
    >>> c #doctest: +ELLIPSIS
    <__main__.C instance at 0x...>

Running ``doctest``
-------------------

To run in a module

>>> import doctest
>>> doctest.testmod() #doctest: +SKIP

To run against a file

>>> import doctest
>>> doctest.testfile('handout.rst') #doctest: +SKIP

``unittest``
=============

unittest: Basic example from python docs
----------------------------------------


>>> import random
>>> import unittest
>>> class TestSequenceFunctions(unittest.TestCase):
...     def setUp(self):
...         self.seq = range(10)
...     def testchoice(self):
...        # note that method begins with "test"
...        element = random.choice(self.seq)
...        self.assert_(element in self.seq)
...
>>> if __name__ == '__main__':
...     unittest.main()

unittest: more details
----------------------

`setUp()` and `tearDown()` are run before each testcase.  

`setUp` should create necessary "fixtures" for testcase (ie populate
database, etc).  `tearDown` should be used to leave environment in
same condition as before the tests were run.

unittest: more details
----------------------

Various `assert*` and `fail*` methods:
  * `assert_(expr [, msg])` - if expr is false signal failure using
    msg.  Also corresponding `failUnless`
  * `assertEqual(first, second [, msg])`
  * `assertNotEqual`
  * `assertRaises(exception, callable, ...)`
  * .... assertBlah, failUnlessBlah....

