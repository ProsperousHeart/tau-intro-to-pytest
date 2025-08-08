**[assertion introspection](https://docs.pytest.org/en/latest/how-to/assert.html#assert-details):**  helpful when trying to figure out why tests fail. Shows you the actual answer

[how to write and report assertions in test](https://docs.pytest.org/en/stable/assert.html)

# Ch 3 - Test Case With Exception

PyTest safely catches any and all unhandled exceptions, performs any cleanup, and moves on to the next test case. Exceptions for one won't affect others.

How to properly verify and handle exceptions in a test case? Use `pytest.raises`

```python
import pytest

# --------------------------------------------------------------------------------
# A test function that verifies an exception
# --------------------------------------------------------------------------------

def test_divide_by_zero():
  with pytest.raises(ZeroDivisionError) as e:
    num = 1 / 0
  
  assert 'division by zero' in str(e.value)
```

In python, **with** is a statement for automatically handling exter enter and exit logic for a caller - most commonly used for I/O. For `pytest.raises`, the logic catches any excceptions and exit logic asserts if the exception type was actually raised. If not, it will raise an assertion error to fail the test.

Makes pytest more concise and avoids repetitive try-except blocks in testing.

Can also verify attributes of raised exception.

Docs:

- [branch](https://github.com/AutomationPanda/tau-intro-to-pytest/tree/chapter/03-exceptions)

- [Assertions about expected exceptions](https://docs.pytest.org/en/stable/assert.html#assertions-about-expected-exceptions)

- [Python errors and exceptions](https://docs.python.org/3/tutorial/errors.html)

- [Python code style](https://docs.python-guide.org/writing/style/)

- [Python’s with statement](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement)

# Ch 4 - Parameterized Test Cases

Sometimes the behaviors we want to test have different inputs/outputs or have specific boundary cases that should be tested.

May be appropriate to "parameterize" to cover all different input/output options.

**Equivalence classes** - each test represents a unique kind of input that yields a unique outcome. A good test suite provides a case for each equivalence class of inputs for a behavior on a test.

Unnecessary tests should be avoided as they add time and cost for little value in return.

Using `@pytest.mark.parametrize` we can take multiple inputs into a single test.
- first argument is a string representing a comma separated list of variable names (must match parameter names for test function)
- second argument is list of parametrized values

```python
# --------------------------------------------------------------------------------
# Imports
# --------------------------------------------------------------------------------

import pytest


# --------------------------------------------------------------------------------
# A most basic test function
# --------------------------------------------------------------------------------

def test_one_plus_one():
  assert 1 + 1 == 2


# --------------------------------------------------------------------------------
# A test function to show assertion introspection
# --------------------------------------------------------------------------------

def test_one_plus_two():
  a = 1
  b = 2
  c = 3
  assert a + b == c


# --------------------------------------------------------------------------------
# A test function that verifies an exception
# --------------------------------------------------------------------------------

def test_divide_by_zero():
  with pytest.raises(ZeroDivisionError) as e:
    num = 1 / 0
  
  assert 'division by zero' in str(e.value)


# --------------------------------------------------------------------------------
# A parametrized test function
# --------------------------------------------------------------------------------

products = [
  (2, 3, 6),            # postive integers
  (1, 99, 99),          # identity
  (0, 99, 0),           # zero
  (3, -4, -12),         # positive by negative
  (-5, -5, 25),         # negative by negative
  (2.5, 6.7, 16.75)     # floats
]

@pytest.mark.parametrize('a, b, product', products)
def test_multiplication(a, b, product):
  assert a * b == product
```

You can take parametrization further with **Hypothesis** - a property-based testing library that can integrate with pytest. You can specify properties of parameter values rather than hard coding them. When tests run, it will crank through several matching values up to 100s or 1,000s of generated tests.

Property-based testing isn't the best approach for all types of testing but certainly worth learning.

Sometimes extra variations are not necessary to cover desired behaviors. Every tuple of inputs is another test, meaning more execution time.

## Resources

- [GitHub repository branch for Chapter 4](https://github.com/AutomationPanda/tau-intro-to-pytest/tree/chapter/04-parametrize)

- [pytest parameters](https://docs.pytest.org/en/stable/parametrize.html#parametrize-basics)

- [More pytest parameters](https://docs.pytest.org/en/stable/example/parametrize.html#paramexamples)

- [Don’t Repeat Yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

- [Python decorators](https://realpython.com/primer-on-python-decorators/)

- [Aspect-Oriented Programming](https://en.wikipedia.org/wiki/Aspect-oriented_programming)

- [Hypothesis](https://hypothesis.readthedocs.io/en/latest/)

# Ch 5 - Unit Test Classes

## Resources

