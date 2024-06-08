## Python Interview Questions and Answers
#### 1. When Python executes the program what things happen?
  1. **Source Code:**
     - You write your Python code in a text editor or an Integrated Development Environment (IDE). The code is saved with a `.py` extension.

  2. **Tokenization and Lexical Analysis:**
     - The Python interpreter reads your source code and breaks it into smaller units called tokens. This is done by the lexer, which identifies keywords, operators, literals, and other elements.
  
  3. **Parsing:**
     - The parser analyzes the tokens and builds a data structure known as the Abstract Syntax Tree (AST). The AST represents the hierarchical structure of your code, showing how statements and expressions relate to each other.
  
  4. **Intermediate Code (Bytecode) Generation:**
     - The Python interpreter then generates an intermediate code, known as bytecode, from the AST. Bytecode is a lower-level representation of your code that is platform-independent.
  
  5. **Execution:**
     - The Python Virtual Machine (PVM) executes the bytecode. The PVM is a part of the Python runtime environment responsible for executing Python programs. It reads the bytecode instruction by instruction and performs the corresponding operations.
  
  6. **Dynamic Typing:**
     - Python is dynamically typed, meaning variable types are determined at runtime. This allows for flexibility but requires extra work during execution to handle type checking.
  
  7. **Importing Modules:**
     - If your program includes imports of other modules or packages, Python will load and execute those modules as needed.
  
  8. **Memory Management:**
     - Python manages memory automatically through a process called garbage collection. Objects that are no longer needed are identified and deallocated to free up memory.
  
  9. **Error Handling:**
     - If an error occurs during execution, Python raises an exception. You can use exception handling constructs (try, except, finally) to handle errors gracefully.
  
  10. **Termination:**
      - Once the program has completed execution or encountered an unhandled error, the Python interpreter terminates. The interpreter may also exit if the program explicitly calls the `exit()` function or encounters a fatal error.
  
  This process provides a simplified overview, and the actual implementation details involve various optimizations and complexities to ensure efficient execution. Keep in mind that Python is an interpreted language, and this process happens each time you run your Python script.
#### 2. Explain decorators in Python and provide an example.

  Decorators are a powerful and flexible way to modify or extend the behavior of functions or methods in Python. They use the @decorator syntax and are applied above the function definition. Decorators are essentially functions that take a function as an argument and return a new function that usually extends or modifies the behavior of the original function.
  ```
  def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Something is happening before the function is called.")
        func(*args, **kwargs)
        print("Something is happening after the function is called.")
    return wrapper

  @my_decorator
  def say_hello():
      print("Hello!")
  
  say_hello()

  def time_decorator(func):
     def wrapper(*args, **kwargs):
         start_time = time.perf_counter_ns()
         func(*args, **kwargs)
         print(f'Time Taken by {func.__name__}: {time.perf_counter_ns() - start_time} ns')
     return wrapper
```

#### 3. What is a generator in Python, and how does it differ from a regular function?
  A generator is a special type of iterable in Python, created using a function with the yield keyword. It allows you to iterate over a potentially large set of data without loading the entire set into memory.
  ##### Generators
  Generators are a type of iterable, similar to lists or tuples, but they allow lazy evaluation of values. Instead of generating all values at once and storing them in memory, a generator produces values on-the-fly using the yield keyword. This can significantly reduce memory consumption and is especially useful when dealing with large datasets.
  ```
  def my_generator():
    yield 1
    yield 2
    yield 3

  gen = my_generator()
  
  for value in gen:
      print(value)
  ```

#### 4. Explain metaclasses in Python.
  Metaclasses are classes for classes. They define how classes behave, and you can think of them as the "class of a class." By defining a metaclass, you can customize the creation of classes, including adding or modifying methods and attributes. Metaclasses are often used in frameworks and libraries to enforce coding standards or conventions.
  ```
  class MyMeta(type):
    def __new__(cls, name, bases, dct):
        # Modify the class before it is created
        dct['custom_attribute'] = 42
        return super().__new__(cls, name, bases, dct)

  class MyClass(metaclass=MyMeta):
      pass

  print(MyClass.custom_attribute)
  ```

#### 5. What is a context manager, and how is it implemented in Python?
  A context manager is an object that defines the methods __enter__() and __exit__(), allowing you to allocate and release resources precisely. It's commonly used with the with statement.
  ```
  class MyContextManager:
    def __enter__(self):
        print("Entering the context")
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

  with MyContextManager() as cm:
      print("Inside the context")
  ```

#### 6. Explain asynchronous programming in Python and provide an example using asyncio.
  Asynchronous programming in Python allows you to write non-blocking code, improving the performance of I/O-bound operations. asyncio is a library for asynchronous programming.
  ```
  import asyncio

  async def my_coroutine():
      print("Start Coroutine")
      await asyncio.sleep(2)
      print("End Coroutine")
  
  # Run the coroutine
  asyncio.run(my_coroutine())
  ```

#### 7. What is the purpose of the __init__ method in Python classes?
The __init__ method is a special method in Python classes and is called when an object is created. It is used to initialize the attributes of the object. It allows you to set default values for attributes and perform any other setup that needs to be done when an object is instantiated.
```
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 30)
print(person.name, person.age)
```

#### 8. Explain the concept of closures in Python.
A closure is a function object that has access to variables in its lexical scope, even when the function is called outside that scope. Closures allow data encapsulation and are often used to create function factories or to implement decorators. They "close over" variables from their containing function, meaning they remember the values of those variables even if they are not in scope.
```
def outer_function(x):
    def inner_function(y):
        return x + y
    return inner_function

closure_instance = outer_function(10)
result = closure_instance(5)
print(result)  # Output: 15
```

#### 9. What is the purpose of the with statement in Python?
The **with** statement is used to simplify resource management, such as file handling or network connections. It ensures that certain operations are performed before and after a block of code, for example, opening and closing a file. The with statement is used with objects that support the context management protocol by implementing __enter__ and __exit__ methods.
```
class CustomContext:
    def __enter__(self):
        print("Entering the context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with CustomContext() as context:
    print("Inside the context")
```

#### 10. Explain the difference between deepcopy and shallowcopy in Python.
**copy.deepcopy** creates a new object and recursively copies the content of the original object along with all nested objects. In contrast, **copy.copy** (shallow copy) creates a new object but does not create copies of the nested objects. Instead, it copies references to the nested objects. Therefore, changes made to nested objects in a shallow copy can affect the original object.
```
import copy

original_list = [[1, 2, 3], [4, 5, 6]]
shallow_copy = copy.copy(original_list)
deep_copy = copy.deepcopy(original_list)

original_list[0][0] = 100

print(original_list)  # Output: [[100, 2, 3], [4, 5, 6]]
print(shallow_copy)   # Output: [[100, 2, 3], [4, 5, 6]]
print(deep_copy)      # Output: [[1, 2, 3], [4, 5, 6]]
```

#### 11. What is the purpose of the asyncio module in Python?
The asyncio module provides support for asynchronous I/O operations in Python. It allows the creation of asynchronous functions and coroutines, enabling efficient handling of concurrent tasks without the need for threads or processes. asyncio is particularly useful in building scalable and responsive network applications.

#### 12. Explain the Global, Local, and Nonlocal keywords in Python.
-  Global: The global keyword is used to indicate that a variable is a global variable, meaning it is accessible throughout the entire program.
-  Local: Variables declared inside a function are local to that function and can only be accessed within that function.
-  Nonlocal: The nonlocal keyword is used to indicate that a variable refers to a variable in the nearest enclosing scope that is not global. It is often used in nested functions.
```
x = 10

def outer():
    y = 20

    def inner():
        nonlocal y
        y += 5
        print(f"Inner function: {x}, {y}")

    inner()
    print(f"Outer function: {x}, {y}")

outer()
print(f"Global scope: {x}")
```

#### 13. Explain the GIL and its impact on multi-threaded Python programs.
The Global Interpreter Lock (GIL) is a mutex that protects access to Python objects, preventing multiple native threads from executing Python bytecode at once. This can limit the performance gain in CPU-bound and multi-threaded programs, as only one thread can execute Python bytecode at a time. However, it doesn't affect performance significantly in I/O-bound tasks.

The GIL is a mechanism used in CPython to synchronize access to Python objects, preventing multiple threads from executing Python bytecode at once. This can impact the performance of multi-threaded programs, especially in CPU-bound tasks, as only one thread can execute Python bytecode at a time. However, it doesn't affect the performance significantly in I/O-bound tasks.

#### 14. Explain the concept of context managers and how they are implemented in Python.
Context managers are objects that define the methods __enter__ and __exit__ to set up and tear down a resource, respectively. They are typically used with the with statement to ensure that resources are properly managed. The contextlib module provides utilities for creating context managers, and the @contextmanager decorator simplifies their creation using generators.
```
class CustomContext:
    def __enter__(self):
        print("Entering the context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with CustomContext() as context:
    print("Inside the context")
```

#### 15. What is monkey patching, and when would you use it in Python?
Monkey patching is the dynamic modification of a class or module at runtime. It is often used to alter or extend the behavior of existing code without modifying its source. While it can be a powerful tool, it should be used cautiously, as it can lead to maintenance issues and unexpected behavior.

#### 16. Explain the use of the __slots__ attribute in Python classes.
The __slots__ attribute is used to explicitly declare a list of attributes for a class. When defined, instances of that class can only have attributes specified in __slots__. This can lead to memory savings and faster attribute access because it avoids the creation of a dynamic dict for each instance.

#### 17. How does Python's garbage collection work?
Python uses automatic memory management through a garbage collector. The primary algorithm is reference counting, where objects are deallocated when their reference count drops to zero. Additionally, Python has a cyclic garbage collector that can identify and collect reference cycles (circular references) by periodically running a cycle detection algorithm.

#### 18. Explain the difference between an iterator and an iterable in Python.
An iterable is any Python object capable of returning its elements one at a time. An iterator is an object representing a stream of data, providing methods like __iter__() and __next__() to iterate through its elements. All iterators are iterables, but not all iterables are iterators. Iterables can be converted to iterators using the iter() function.

#### 19. Compare and contrast threads and processes in Python. Provide an example of using threads.
Threads and processes are used for concurrent execution. Threads share the same memory space, while processes have separate memory spaces.

#### 20. Singleton in Python.
```
class Singleton:
  _instance = None

  def __new__(cls, *args, **kwargs):
    if cls._instance is None:
        cls._instance = super().__init__(cls)
        cls._instance.__init__(*args, **kwargs)

    return cls._instance
```

#### 21. Find the longest unique substring.
a = "abcdefghabc"
```
def longest_substring(s):
    ix_map = {} # char with index
    start, max_length = 0, 0 # start, max_length
    for i, char in enumerate(s):
        if char in ix_map and ix_map[char] >= start:
            start = ix_map[char] + 1
        ix_map[char] = i
        curr_len = i - start + 1
        max_length = max(max_length, curr_len)
  
    return max_length
```


#### 22. We are given that the string "abc" is valid. From any valid string V, we may split V into two pieces X and Y such that X + Y (X concatenated with Y) is equal to V.  (X or Y may be empty.)  Then, X + "abc" + Y is also valid. should be equals to V. If for example S = "abc", then examples of valid strings are: "abc", "aabcbc", "abcabc","ababcc". Examples of invalid strings are: "abccba", "ab", "cababc", "bac".Return true if and only if the given string S is valid
##### Test Cases:
###### print(is_valid("abc"))  # Returns: True
###### print(is_valid("aabcbc"))  # Returns: True
###### print(is_valid("abcabc"))  # Returns: True
###### print(is_valid("abccba"))  # Returns: False
###### print(is_valid("ab"))  # Returns: False
###### print(is_valid("cababc"))  # Returns: False
###### print(is_valid("bac"))  # Returns: False

```
def is_valid(s):
     
    while "abc" in s:
        s = s.replace("abc", "")

    return not s
```

#### 23. Create a DataFrame and save it as csv using pandas.
```
import pandas as pd

data = {
    "name": ["a", 'b', "c"],
    "age": [1, 2, 3]
}

df = pd.DataFrame(data)

df.to_csv("test.xlsx")
```

#### 24. Create a FastAPI app to identify if a give website is working or not.
```
from fastapi import FastAPI
import requests

app = FastAPI()

@app.post("/check-website")
def check_website(url: str):
    response = requests.get(url=url)
    if response.status_code == 200:
        return f"{url} is available"
    return f"{url} is unavialable"
```
**command to run:** uvicorn \<filename\>:app --port 8000 --reload


#### 25. Give the output for the following program.
```
class A:
    value = 1

class B(A):
    pass

class C(B):
    pass
```

**CASE I:** print(A.value, B.value, C.value)   
**CASE II:**     
    C.value = 2   
    print(A.value, B.value, C.value)   
**CASE III:**   
    B.value = 2   
    print(A.value, B.value, C.value)   
**CASE IV:**   
    A.value = 2   
    print(A.value, B.value, C.value)    

**Result**   
**CASE I:** 1 1 1    
**CASE II:** 1 1 2   
**CASE III:** 1 2 2   
**CASE IV:** 2 2 2   

#### 26. Give the output for the following program.
```
class A:
    value = 1

class B:
    value = 2

class C(B, A):
    pass

print(C.value)
```
#### **Result:** 2
