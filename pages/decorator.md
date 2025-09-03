- > 装饰器（decorator）是 Python 的一个重要特性，主要用于修改或增强函数或类的行为。
-
- 装饰器可以让你在不修改原函数代码的前提下，增加函数的新的行为或者修改函数的行为。你可以对任何函数或方法使用装饰器，装饰器也可以接受参数，这使得装饰器在 Python 语言中变得非常强大和灵活。
-
- 下面是一个基本的装饰器使用示例：
- ```python
  def my_decorator(func):
      def wrapper(*args, **kwargs):
          print("Something is happening before the function is called.")
          func(*args, **kwargs)
          print("Something is happening after the function is called.")
      return wrapper
  
  @my_decorator
  def say_hello(name):
      print(f"Hello! {name}")
  
  say_hello("fengfeng")
  ```
-
-