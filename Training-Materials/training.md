**[assertion introspection](https://docs.pytest.org/en/latest/how-to/assert.html#assert-details):**  helpful when trying to figure out why tests fail. Shows you the actual answer

[how to write and report assertions in test](https://docs.pytest.org/en/stable/assert.html)

# Ch 3 - TEst Case With Exception

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

# Ch 4 - 