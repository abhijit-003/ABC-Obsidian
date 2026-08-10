# Python Roadmap (Java -> Python)

## 1. Basics
- Installation
- REPL
- Indentation
- Comments
- Variables (Dynamic Typing)
- Input/Output
- Naming Conventions
---
## 2. Data Types
### Primitive
- int
- float
- bool
- complex

### Collections
- str
- list
- tuple
- set
- dict
- bytes

Concepts
- Mutable vs Immutable
- Type Conversion
- id(), type()

---

## 3. Operators
- Arithmetic
- Assignment
- Comparison
- Logical
- Bitwise
- Membership (`in`, `not in`)
- Identity (`is`, `is not`)

---

## 4. Control Flow
- if
- elif
- else
- Ternary Operator
- match-case (Python 3.10+)

Loops
- for
- while
- break
- continue
- pass
- range()

---

## 5. Strings
Methods
- len()
- split()
- join()
- replace()
- strip()
- find()
- index()
- count()
- upper()
- lower()
- title()
- capitalize()
- startswith()
- endswith()

Formatting
- f-strings
- format()

Concepts
- Slicing
- String Immutability

---

## 6. Lists
Operations
- append()
- extend()
- insert()
- remove()
- pop()
- clear()
- copy()
- reverse()
- sort()

Concepts
- Indexing
- Slicing
- Nested Lists
- List Comprehension

---

## 7. Tuples
- Creation
- Packing
- Unpacking
- Immutability

---

## 8. Sets
Operations
- add()
- remove()
- discard()
- union()
- intersection()
- difference()
- symmetric_difference()

---

## 9. Dictionaries
Operations
- get()
- keys()
- values()
- items()
- update()
- pop()
- popitem()
- clear()

Concepts
- Dictionary Comprehension

---

## 10. Functions
- def
- return
- Scope
- Default Arguments
- Keyword Arguments
- Positional Arguments
- *args
- **kwargs
- Lambda
- Nested Functions
- Recursion

---

## 11. Modules & Packages
- import
- from ... import
- as
- Custom Modules
- Packages
- __name__
- if __name__ == "__main__"

---

## 12. Exception Handling
- try
- except
- else
- finally
- raise
- Custom Exceptions

---

## 13. File Handling
- open()
- with
- read()
- readline()
- readlines()
- write()
- writelines()
- append()

Modes
- r
- w
- a
- rb
- wb

JSON
CSV

---

## 14. OOP
- Class
- Object
- self
- __init__()
- Instance Variables
- Class Variables
- Methods
- Inheritance
- Method Overriding
- super()
- Encapsulation
- Polymorphism
- Abstraction
- Multiple Inheritance
- MRO

Magic Methods
- __str__()
- __repr__()
- __len__()
- __eq__()

Decorators
- @staticmethod
- @classmethod
- @property

---

## 15. Advanced Python
- Iterators
- Generators
- yield
- Decorators
- Closures
- Context Managers
- Namespaces
- LEGB Rule
- Duck Typing

---

## 16. Functional Programming
- map()
- filter()
- reduce()
- lambda
- zip()
- enumerate()
- any()
- all()
- sorted()
- reversed()

---

## 17. Collections Module
- Counter
- defaultdict
- deque
- namedtuple
- OrderedDict

---

## 18. itertools
- product()
- permutations()
- combinations()
- combinations_with_replacement()
- groupby()
- cycle()
- chain()
- accumulate()

---

## 19. heapq
- heapify()
- heappush()
- heappop()
- heappushpop()
- nlargest()
- nsmallest()

---

## 20. bisect
- bisect_left()
- bisect_right()
- insort()

---

## 21. Regex (re)
- match()
- search()
- findall()
- finditer()
- split()
- sub()
- Groups
- Quantifiers
- Character Classes

---

## 22. Type Hinting
- int
- str
- list
- dict
- tuple
- Optional
- Union
- Any
- Generic
- Type Alias

---

## 23. Dataclasses
- @dataclass
- field()

---

## 24. Virtual Environment
- venv
- pip
- requirements.txt
- pip freeze
- pip install
- pip uninstall

---

## 25. Testing
- unittest
- pytest
- Assertions
- Fixtures
- Mocking (Basics)

---

## 26. Concurrency
- threading
- multiprocessing
- asyncio
- async
- await

---

## 27. Logging
- logging
- Levels
- Formatter
- File Logging

---

## 28. Pythonic Features
- List Comprehension
- Dictionary Comprehension
- Set Comprehension
- Generator Expression
- Multiple Assignment
- Tuple Unpacking
- enumerate()
- zip()
- Walrus Operator (:=)
- Context Manager
- EAFP vs LBYL

---

## 29. Useful Standard Libraries
- math
- random
- statistics
- datetime
- time
- os
- pathlib
- shutil
- sys
- re
- json
- csv
- collections
- itertools
- functools
- heapq
- bisect
- typing
- dataclasses

---

## 30. DSA-Specific Libraries (Must Know)
- collections
- heapq
- bisect
- itertools
- math
- functools

---

# Java → Python Mapping

| Java | Python |
|------|---------|
| ArrayList | list |
| HashMap | dict |
| HashSet | set |
| Queue | collections.deque |
| LinkedList | deque |
| PriorityQueue | heapq |
| Arrays.sort() | sorted(), sort() |
| StringBuilder | ''.join(list) |
| Optional | None |
| Streams | map(), filter(), comprehensions |
| static | @staticmethod |
| final | typing.Final |
| interface | ABC / Duck Typing |

---

| Day | Topics                                                                                                                                       |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Syntax, Variables, Data Types, Operators                                                                                                     |
| 2   | Strings, Lists, Tuples, Sets, Dictionaries                                                                                                   |
| 3   | Functions, Modules, Exceptions                                                                                                               |
| 4   | File Handling, OOP                                                                                                                           |
| 5   | Advanced Python (Decorators, Generators, Iterators, Comprehensions)                                                                          |
| 6   | Collections, heapq, bisect, itertools                                                                                                        |
| 7   | Regex, Dataclasses, Type Hinting, Logging                                                                                                    |
| 8   | Virtual Environments, pip, Testing                                                                                                           |
| 9   | Concurrency (threading, multiprocessing, asyncio), Pythonic patterns                                                                         |
| 10  | Solve 30–40 Python coding problems (arrays, strings, hash maps, stacks, queues) to become comfortable with the language before moving to DSA |
