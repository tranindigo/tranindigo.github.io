---
title: "Memoization in Ruby and Python"
date: "2020-09-04"
categories: 
  - "optimization"
  - "python"
tags: 
  - "memoization"
  - "ruby"
---

Memoization refers to remembering results of method calls based on the method inputs and then returning the remembered result rather than computing the result again. You can think of it as a cache for method results but, unlike a cache, memoization doesn't persist across different sessions and instances.

The thing that I really like about Ruby is that it has a streamlined way to memoize method calls. In Ruby, the most common pattern for memoizing a call is using the conditional assignment operator, like so:

```ruby
def current_user
  @current_user ||= User.find(session[:user_id])
end
```

This says that if the `current_user` variable is `nil`, then call `User.find(session[:user_id])`. Otherwise, if the variable already exists, then we can just reuse the value of the variable. This has the same meaning as:

```ruby
def current_user
  @current_user = @current_user || User.find(session[:user_id])
end
```

You should memoize when you've got duplicated database calls, when you have expensive calculations (i.e. the Fibonacci sequence), or when you've got repeated calculations that don't change.

Python has a streamlined way to memoize functions using the `@memoize` decorator. For instance:

```ruby
@memoize
def fibonacci(n):
  if n in (0, 1):
    return n
  return fibonacci(n-1) + fibonacci(n-2)
```

This `fibonacci` function is an expensive calculation, so it makes sense to memoize it. You can also call `memoize(fibonacci(n))` in order to memoize a function call, anonymous function (or lambda). This `memoize` function is available in the decorator library, which is part of many standard Python distributions.

Another way of memoizing in Python is by using objects. For instance, the following class has a `cache` class variable that is shared by all instances of `Fib`. It stores the result of the dunder method `__call__`. When you use the `__call__` method, the dunder method makes instance of `Fib` behave syntactically like functions.

```python
class Fib():
  cache = {}
  def __call__(self, n):
    if n in self.cache:
      ans = self.cache
    if n <= 2:
      ans = 1
      self.cache = ans
    else:
      ans = self(n - 2) + self(n - 1)
      self.cache = ans
    return ans
```

So, as you can see, Python has many ways of implementing memoization. However, I consider these methods to be less streamlined than the clean, conditional expression that Ruby has. At the end of the day, it's your choice which one you want to use!
