---
title: Python Arguments __defaults__
date: 2017-02-04
---

There is an interesting <a href="https://docs.python.org/dev/tutorial/controlflow.html#more-on-defining-functions">example</a> in the Python docs:

```python
# Python 3.5
def f(a, L=[]):
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))
# [1, 2, 3]
```

You can see how the arguments get stored within <code>__defaults__</code> in the snippet below:

<img src="/files/python-defaults.png" width="333" height="373" alt="Python __defaults__" />
