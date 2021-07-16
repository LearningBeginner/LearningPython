# Functions, Parameters, Arguments
## Forcing the Separation of Argument Types
```py
# python 3.8
def func(p0, /, p1, *, p2):
    print(p0, '/sep/', p1, '/sep/' p2)
func(0, p1=0)
func(0, 0, p2=0)

# errors : 
# func(p0=0, p1=0, p2=0)
# func(0, 0, 0)
```
## Packing and Unpacking
```py
def f1(p0, p1):
    print(p0, p1)
f1(p0, p1)
f1(*(p0, p1))
f1(*[p0, p1])

def sum_average(*scores):
    # tuple or list
    num = len(scores)
    return sum(scores) / num

def sum_average_name(**dscores):
    # dictionary
    num = len(dscores)
    sum_ = 0; t_score = -1
    for name, score in dscores.items()
        sum_ += score
        if score > t_score:
            t_score = score; t_name = name
    print(num, sum_, sum_ / num)
```

# Name Spaces within a Module
```py
x = 'Initial Global'
def func0():
    print(f"<func0> x: {x}.")
def func1():
    x = "L in func1"
    print(f"<func1> x: {x}.")
def func2():
    global x
    print(f"<func2-1> x: {x}.")
    x = "G in func2"
    print(f"<func2-2> x: {x}.")
def func3():
    y = "L in func3"
    print(f"<func3-1> x: {x}; y: {y}.")
    def func4():
        print(f"<func4> x: {x}; y: {y}.")
        def func5():
            nonlocal y
            x = "L in func5"
            print(f"<func5-1> x: {x}; y: {y}.")
            y = "L in func5"
            print(f"<func5-2> x: {x}; y: {y}.")
        func5()
    func4()
    print(f"<cunc3-2> x: {x}; y: {y}.")
func0()
func1()
func2()
func3()
# <func0> x: Initial Global.
# <func1> x: L in func1.
# <func2-1> x: Initial Global.
# <func2-2> x: G in func2.
# <func3-1> x: G in func2; y: L in func3.
# <func4> x: G in func2; y: L in func3.
# <func5-1> x: L in func5; y: L in func3.
# <func5-2> x: L in func5; y: L in func5.
# <cunc3-2> x: G in func2; y: L in func5.
```

# Data Structures
```py
from colletions import deque
que = deque()
que.append(0)
que.appendleft(0)
que.popleft()
que.pop()
que2 = deque([1,4,5])
```
# Elementary functions
```py
A = sorted(['the', 'hello', 'beetlejuice', 'pear'], key=len)
# you can check orders ord('0'), ord('a'), ...
B = list(map(lambda x: x ** 2, [1, 2, 3]))
C = list(map(lambda x, y: x ** 2 + y ** 2, [1, 2, 3], [100, 200, 300]))
D = list(map(lambda x, y: x ** 2 + y ** 2, [1, 2, 3], [100, 200, 300, 400]))
# C == D

from functools import reduce
def add_two(x, y):
    return x + y

10 == reduce(add_two, (1, 2, 3, 4))
20 == reduce(add_two, (1, 2, 3, 4), 20)
```

# Command Line Parsing
```py
from optparse import OptionParser
import sys

usage = "usage: %prog [-r num_runs] "
parser = OptionParser(usage=usage)
parser.add_option('-p', '--prog_tr', action='store_true', default=False, dest='program_trace',
                  help='enable the original trace of the decorated program')
# ...
# ...

(options, args) = parser.parse_args()
program_trace = options.program_trace
num_runs = options.num_runs

arg_len = len(args)
if arg_len > 0:
    if (arg_len > 1) or (not args[0].isdigit()):
        parser.print_help()
        sys.exit(0)
    num_runs = int(args[0])
```
## Format specification Mini Language
```
replacement_field::=  "{" [field_name] ["!" conversion] [":" format_spec] "}“
field_name  ::=  arg_name("." attribute_name| "[" element_index"]")*
arg_name  ::=  [identifier | digit+]
attribute_name ::=  identifier
element_index ::=  digit+ | index_string
index_string ::=  <any source character except "]"> +
conversion        ::=  "r" | "s" | "a“
format_spec ::=  “next page”

format_spec ::=  [[fill]align][sign][#][0][width][grouping_option][.precision][type]
fill            ::=  <any character>
align           ::=  "<" | ">" | "=" | "^“
sign            ::=  "+" | "-" | " “
width           ::=  digit+
grouping_option ::=  "_" | ",“
precision       ::=  digit+
type            ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"
```