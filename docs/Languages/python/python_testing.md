<h1>Python Testing</h1>

[TOC]

# Testing Framework

## Possible Ways Of Doing
* Python
    * Using assert; no module require
    * Using assert with setup_module(module) & teardown_module(module) methods for resource setup (define global variables)
    * unittest framework
        * class level: 
            * inherit unittest.TestCase
            * override setUP(self) method for resource setup as class members
            * use self.assertEqual(var1, var2) or self.assertNotEqual(var1, var2)
    * pytest framework
        * by functions: using assert & @pytest.fixture(scope="module") for resource setup
        * by classes: (define all test cases inside) using assert & @pytest.fixture(scope="class") for resource setup
* Django
    * Using django.test
        * from django.test import TestCase
        * same as unittest
        * define class and inherit TestCase
        * define test_cases(self) method
        * use self.assertIs(var, bool)
        

## 1. unittest Testing Framework

### Intro
* Inbuilt 
* Class based
* import class unittest.TestCase
* define setUp method for setup resources
* define testcase method for assertion/testing
* execution: run the module or python -m unittest test_module_name.py
* **Note:** Module & method should have 'test_' prefix & class have 'Test' prefix
* e.g.

```python
import unittest
try:
    from .binary_tree import in_order, Node
except:
    from binary_tree import in_order, Node


class TestBinaryTree(unittest.TestCase):
    def setUp(self):
        self.root = Node(1)
        self.root.left = Node(2)
        self.root.right = Node(3)
        self.root.left.left = Node(4)
        self.root.left.right = Node(5)
        self.result = []
        self.func_in_order = in_order(self.root, self.result)

    def test_in_order_positive(self):
        self.assertEqual(self.func_in_order, [4, 2, 5, 1, 3], msg=None)


    def test_in_order_negative(self):
        self.assertNotEqual(self.func_in_order, [], msg=None)


if __name__ == '__main__':
    root = None
    unittest.main()
```

### mock Library (Python 2.x) & unittest.mock Library (Python 3.x)
#### Intro
unittest.mock is a library for testing in Python. It allows us to replace parts of our system under test with mock objects and make assertions about how they have been used.

It is based on the 'action --> assertion' pattern instead of 'record --> replay' used by many mocking framework.

#### Features

* Mock class
* patch() decorator
* MagicMock class

#### Why
* **Increased speed â **
Tests that run quickly are extremely beneficial. E.g. if you have a very resource intensive function, a mock of that function would cut down on unnecessary resource usage during testing, therefore reducing test run time.

* **Avoiding undesired side effects during testing â **
If you are testing a function which makes calls to an external API, you may not want to make an actual API call every time you run your tests. You'd have to change your code every time that API changes, or there may be some rate limits, but mocking helps you avoid that.

## 2. pytest Framework

* **Introduction:**
    * The pytest framework makes it easy to write small tests, yet scales to support complex functional testing for applications and libraries.

* **Source:**
    * https://pypi.python.org/pypi/pytest/3.2.3
    * https://docs.pytest.org/en/latest/contents.html#toc

* **Installation:**
    * pip install pytest

* **execution:**
    * execute: pytest pytest_ex1.py
    
### Types

#### assert 
It's an standard python statement for verifying expectations and values.
Input type: logical conditions
Output:
* Nothing/blank, if true
* Raise AssertionError exception, if false

e.g.

```python
# py-misc/py-testing-examples/pytest_ex1.py

def add(x, y):
    return x + y

def test_add_positive():
    assert add(3,4) == 7
    
def test_add_negative():
    assert add(3,3) == 7  
```    

#### Running multiple tests
pytest will run all files in the current directory and its subdirectories of the form test_*.py or *_test.py. More generally, it follows standard test discovery rules.

#### Asserting that a certain exception is raised
If you want to assert that some code raises an exception you can use the raises helper:
```python
# content of pytest_ex2.py
import pytest
def f():
    raise SystemExit(1)

def test_mytest():
    with pytest.raises(SystemExit):
        f()
```        


#### Grouping multiple tests in a class
Once you start to have more than a few tests it often makes sense to group tests logically, in classes and modules. Letâs write a class containing two tests:

```python
# content of test_class.py
class TestClass(object):
    def test_one(self):
        x = "this"
        assert 'h' in x

    def test_two(self):
        x = "hello"
        assert hasattr(x, 'check')
```   


The two tests are found because of the standard Conventions for Python test discovery. There is no need to subclass anything. We can simply run the module by passing its filename:

```bash
pytest -q test_class.py
```

### Resource Setup

1. setup & teardown (classic xunit style)
2. fixture (recommended)
    * complies with dependency injection

### Features

1. Detailed informations on assert statements
2. Auto-discovery of test modules and functions **to study**
3. Modular fixtures for managing small or parameterized long-lived test resources **to study**


## 3. coverage.py Tool

### Intro
* a tool for measuring code coverage of Python programs
* It monitors your program, noting which parts of the code have been executed, then analyzes the source to identify code that could have been executed but was not
* **Use**
    * typically used to gauge the effectiveness of tests. 
    * It can show which parts of your code are being exercised by tests, and which are not.
    
### Quick Start

1. Install using

    ```bash
    pip install coverage
    ```
2. run the module

    ```bash
    coverage run my_program.py arg1 arg2
    ```
3. get coverage report

    ```bash
    coverage report -m
    ```

4. get coverage report in html 

    ```bash
    coverage html
    ```

