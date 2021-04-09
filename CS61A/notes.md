# CS61A
cs61a is a course about managing complexity(mastering abstraction and programming paradigms). it's an introduction to programming(after the class, you can get a full understanding of python fundamentals, combine multiple ideas in large projects, and understand how computers interpret programming languages).

## 目录
1. [Getting Started](#getting-started)
   1. [vscode](#vscode)   
   2. [unix commands](#unix-commands)
   3. [python command line options](#python-command-line-options)
   4. [special need](#special-need)
   5. [doing assignments](#doing-assignments)
2. [Building Abstractions With Functions](#building-abstractions-with-functions)
   1. [elements of programming](#elements-of-programming) 
   2. [defining functions](#defining-functions)
   3. [designing functions](#designing-functions)
   4. [higher order functions](#higher-order-functions)

## Getting Started
computer science is the study of *what* problems can be solved using computation, *how* to solve those problems, and what techniques lead to *effective* solutions.

fucntions encapsulate logic that manipulate data. functions are the primary topic of chapter 1.  
objects seamlessly bundle together data and the logic that manipulates that data. objects are the primary topic of chapter 2.  
the design and implementation of interpreters is the primary topic of chapter 3.

computer = powerful + stupid

### vscode
open vscode in the current working directory via command line:  
```
code .
```

`tab`: indent a line or a group of lines  
`shift-tab`: dedent a line or a group of lines 
`commad-d`: highlights the current word. This allows you to easily rename variables with multiple cursors!  
`command-z`: undo  
`command-shift-z`: redo
`command-s`: save the current file  
 
### unix commands
directories: `ls`, `mkdir`, `cd`(`cd`, `cd ~`, `cd .`, `cd ..`), `rm -r`.    
files: `cat`(display), `mv`(move contents or rename), `cp`(copy), `rm`.  
miscellaneous: `echo`(display words on the screen), `man`(displays manual pages for a specified command).  

### python command line options
`-h`: Print a short description of all command line options.  
`-V`: Print the Python version number and exit.  
`-v`: display the process of running doctests.
```
python3 -m doctest -v file.py
```
`-m doctest`: run doctests.  
```
python3 -m doctest file.py
```  
`-i`: make python to start in interactive mode. In an interactive mode, you can run Python code line by line and get immediate feedback instead of running an entire file all at once.  
```
python3 -i file.py
```  

### special need
**add a directory to path**  
step 1: tape the following in the terminal to open the file needed.
```zsh
nano ~/.zshrc
```
step 2:
```zsh
export PATH="${PATH}:<path to directory>"
export PYTHONPATH="${PYTHONPATH}:<path to directory>"
```
step 3: follow the instruction below to exit; save the file and restart the terminal.

### doing assignments
*predicting problems*  
enter the following in the terminal:
```
python3 ok -q <filename> -u
```

*function writing problems*  
writing code in text editor, save it, then open terminal, drop to the required directory, and run ok with this command:
```
python3 ok
```

*debugging using ok*  
open an interactive terminal to investigate a failing test for question.
```
python3 ok -q <question name> -i
```
open an enviroment diagram to investigate a failing test for question.
```
python3 ok -q <question name> --trace
```

## Building Abstractions With Functions
### elements of programming
computer programs consist of instructions to either
- compute some value
- carry out some action
*statements typically describe actions, while expressions typically describe computations.*
In general, statements are not evaluated but executed, while expressions are evaluated but not executed.

every powerful language has three such mechanisms:
- primitive expressions and statements
- means of combination, by which compound elements are built from simpler ones
- means of abstraction, by which compound elements can be named and manipulated as units

types of elements: *functions and data*. Thus, any powerful programming language should be able to describe primitive data and primitive functions, as well as have some methods for combining and abstracting both functions and data.

#### expressions
types of expressions:  
1. primitive expressions: number(2), name(add), string('hello').  
2. compound expressions
   - use infix notation
   - use function notation -- **call expressions**
   ```
   operator(operand, operand)  
   ```
   evaluation procedure:  
   1. Evaluate the operator subexpressions and then the operand subexpressions.  
   2. Apply the function that is the value of the operator to the arguments that are the values of the operands.
   ```
   >>> (lambda: 3)()
   3
   ```
Function notation has three principal advantages over the mathematical convention of infix notation.

#### statements
**assignment statements** -- bound names to value  
execution rule:  
1. Evaluate *all* expressions to the *right* of "=", from left to right. 
2. Bind all names to the left of "=", to those resulting values in the current frame(each name can only be bound to *one* value). 

swapping the values bound to two names can be perfomed in a single statements:
```
y, x = x, y
```
Assignment is the simplest means of abstraction.   

**conditional statements**  
syntax tips:  
1. alwanys starts with "if" clause
2. then zero or more "elif" clauses
3. then zero or one "else" clause. always at the end

only one **kind** of clause may be executed.  
```
>>> def just_in_case():
        x = 10
        if x > 0:
            x += 2
        if x < 13:
            x += 3
        if x % 2 == 1:
            x += 4
        return x
>>>> just_in_case()
19
```     

**conditional expressions**  
```
>>> x = 0
>>> abs(1/x if x!=0 else 0)
0
```

**boolean context**  
- false values: `False`, `0`, `''`, `[]`, `None`
- true values: anything else

- built-in comparison operators(>, <, >=, <=, ==, !=) return boolean values(`True` or `False`).  
- logical operators(*or, and, not*) -- priority from lowest to highest, the last two return the last *value* they evaluate.
```
>>> 1 and 3 and 6 and 10 and 15
>>> 15
>>>
>>> -1 and 1 > 0
>>> True
```

Functions that perform comparisons and return boolean values typically begin with is, not followed by an underscore (e.g., isfinite, isdigit, isinstance).

**iteration**
when there is a infinite loop, press `<control>-c` to force Python to stop looping.

### defining functions 
a function consists of its *signature* and body:
```
def <name>(<formal parameters>):
    return <return expression>
```

execution procedure:  
1. create a function with signature
2. set the body of that function to be everything indented after the first line
3. *bind <name>* to that function in the current frame 

procedure for calling user-defined functions:
1. Add a local frame, forming a new environment
2. bind the function's formal parameters to its arguments *in that frame* 
3. Execute the body of the function in that new environment

bind name to parameter in a local frame; name of funtion vs. function -- `b` vs. `func b(b,x)`.   
```
>>> a = lambda x: x * 2 + 1
>>> def b(b, x):
        return b(x + a(x))
>>> x = 3
>>> b(a, x)
21
```

#### docstring
which must be indented along with the function body. The first line describes the job of the function in one line, followed by a blank line. The following lines can describe arguments and clarify the behavior of the function.

When writing Python programs, include docstrings for all but the simplest functions. Remember, code is written only once, but often read many times. 

#### environments
The possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an environment.

an environment is a sequence of frames.

everytime a defined function is called in the global frame, a new local frame is created.(which means if a function is called *again*, it won't jump to the previous frame but will create a new frame)  

the parent frame of a function is the frame where it was defined, not called.

variable lookup procedure:
1. look in the current frame
2. if not found, recursively look in the parent frame
3. till the global frame, if not found, Error

A *scope* defines the visibility of a name within a block. If a local variable is defined in a function block, the scope *extends to any blocks contained within the defining one*(lexical scope), unless a contained block introduces a different binding for the name -- assignment statements make variables a local variable, which would change it's scope.

a `UnboundLocalError`comes out when executing line A:
```
>>> def f(x):
        def g(y):
            return y + 1     #line A
            x += 1           #line B
        return g
>>> f(2)(3)
```

### designing functions 
- give each function exactly one job. but make it apply to many related situations. 
- don't repeat yourself. implement a process just once, but execute it many times.
- define functions generally. 
  - generalization: find the common stucture among similar related problems, which may be a number, or more likely, a computational process
- gradually forming a habit of coding to make code more **readable and clear**.

#### functional abstractions 
give a name to some computational process, and then referring to that process as a whole without worrying about it's implementation details.  

Understanding functional abstractions via their *domain, range, and intent* is critical to using them correctly in a complex program.

#### pure functions & non-pure functions
- pure functions: just return values  
- non-pure functions: have side effects -- will print sth

Imposing restrictions of pure functions yields substantial benefits.

**return & print**  
- the value that print returns is always None
- the interactive Python interpreter does not automatically print the value None
- no return no value, no print no output
- values and outputs go absolutly different way, one float, one flop
```
>>> x = None
>>> x
>>>


>>> def what_prints():
       print('ok')
       return 'ok'
   
>>>what_prints()
ok
'ok'
```
#### debugging
debugging techniques:  
1. read error messages: from the last line to the first line(upwards).
2. running doctests:
3. writing testing functions
4. using `print` statements
   - add some message to make it easier to read
   ```
   print('debug: tmp was this:', tmp)
   ```
   - long-term debugging
   ```
   debug = True
   def foo(n):
       i = 0
       while i < n:
           i += func(i)
           if debug:
               print('debug: i is', i)
   ```
5. using interactive mode
6. using python tutor
7. using assert statements
   -  An assert statement has an expression in a boolean context, followed by a quoted line of text (single or double quotes are both fine, but be consistent) that will be displayed if the expression evaluates to a false value.
   ``` 
   >>> assert fib(8) == 13, 'the 8th fibonacci number should be 13'
   ```

it's better to crash than to get an incorrect result.

guiding principles of debugging
1. test incrementally
2. isolate errors
3. check your assumptions
4. consult others

**error types**  
`SyntaxError`, `IndentationError`(a tab could be a different number of columns depending on the environment, but a space is always one column. to be consistent, use spaces over tabs!), `TypeError`, `NameError`, `IndexError`.  

`EOL` stands for "end of line".

### higher order function 
a function that manipulates other functions by taking in functions as argument values, returning functions as return values, or both.
```
def cube(k):
    return pow(k, 3)

def summation(n, term):
    """sum the first n terms of a sequence.
    >>>> summation(5, cube)
    225
    """
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total
    
    
def make_adder(n):
    """return a function that takes one argument k and return k + n.
    >>> add_three = make_adder(3)
    >>> add_three(4)
    7
    >>> make_adder(3)(4)
    7
    """
    def adder(k):
        return k + n
    return adder
``` 

Elements with the fewest restrictions are said to have *first-class status*. Python awards functions full first-class status. some of the "rights and privileges" of first-class elements are:
1. They may be bound to names.
2. They may be passed as arguments to functions.
3. They may be returned as the results of functions.
4. They may be included in data structures.

#### self-reference 
return a function using it's own name.
```
def print_sums(n):
    """
    >>> print_sums(1)(3)(5)
    i
    4
    9
    """
    print(n)
    def next_sum(k):
        return print_sums(n + k)
    return next_sum
```

#### currying
transform a multi-argument function into a single-argument, higher-order function.
```
>>> add(2, 3)
5
>>> make_adder(2)(3)
5
```

#### function decorators
apply higher-order functions as part of executing a def statement.
```
>>> def trace(fn):
        def wrapped(x):
            print('->', fn, '(', x, ')')
            return fn(x)
        return wrapped

>>> @trace
    def triple(x):
        return 3 * x
        
>>> triple(12)
-> <function triple at 0x102a39848> ( 12 )
36
```
which is equivalent to :
```
>>> def triple(x):
        return 3 * x
        
>>> triple = trace(triple)
```

decorators are used for tracing, as well as selecting which functions to call when a program is run from the command line.            
    
#### lambda expressions
a function with formal parameter x that returns the value of `x * x`.(a annoymous function -- func λ(x), a shorthand way of writing a def statement)
```
lambda x: x * x
```
bind the function to a name(`square` is not the intrinsic name).
```
square = lambda x: x * x
```

```
>>> x = 10
>>> square = x * x
>>> square
100

>>> square = lambda x: x * x
>>> square(10)
100
>>> (lambda x: x * x)(10)
100

>>> def square(x):
    return x * x
>>> a = square
>>> a(10)
100


>>> b = lambda x: lambda: x
>>> c = b(88)
>>> c
<function <lambda>.<locals>.<lambda> at 0x7ff62e2781f0>
>>> c()
88

>>> def f():
        return 13
>>> (lambda y: y())(f)
13
```

## summary(attention！) 
- think procedurally!
- in a program, what most of code's doing are just manipulating names and calling functions. 
- programs must be written for people to read, and only incidentally for machines to execute.


# CS61A
cs61a is a course about managing complexity(mastering abstraction and programming paradigms). it's an introduction to programming(after the class, you can get a full understanding of python fundamentals, combine multiple ideas in large projects, and understand how computers interpret programming languages).

## 目录
1. [Getting Started](#getting-started)
   1. [vscode](#vscode)   
   2. [unix commands](#unix-commands)
   3. [python command line options](#python-command-line-options)
   4. [special need](#special-need)
   5. [doing assignments](#doing-assignments)
2. [Building Abstractions With Functions](#building-abstractions-with-functions)
   1. [elements of programming](#elements-of-programming) 
   2. [defining functions](#defining-functions)
   3. [designing functions](#designing-functions)
   4. [higher order functions](#higher-order-functions)

## Getting Started
computer science is the study of *what* problems can be solved using computation, *how* to solve those problems, and what techniques lead to *effective* solutions.

fucntions encapsulate logic that manipulate data. functions are the primary topic of chapter 1.  
objects seamlessly bundle together data and the logic that manipulates that data. objects are the primary topic of chapter 2.  
the design and implementation of interpreters is the primary topic of chapter 3.

computer = powerful + stupid

### vscode
open vscode in the current working directory via command line:  
```
code .
```

`tab`: indent a line or a group of lines  
`shift-tab`: dedent a line or a group of lines  
`commad-d`: highlights the current word. This allows you to easily rename variables with multiple cursors!  
`command-z`: undo  
`command-shift-z`: redo
`command-s`: save the current file  
 
### unix commands
directories: `ls`, `mkdir`, `cd`(`cd`, `cd ~`, `cd .`, `cd ..`), `rm -r`.    
files: `cat`(display), `mv`(move contents or rename), `cp`(copy), `rm`.  
miscellaneous: `echo`(display words on the screen), `man`(displays manual pages for a specified command).  

### python command line options
`-h`: Print a short description of all command line options.  
`-V`: Print the Python version number and exit.  
`-v`: display the process of running doctests.
```
python3 -m doctest -v file.py
```
`-m doctest`: run doctests.  
```
python3 -m doctest file.py
```  
`-i`: make python to start in interactive mode. In an interactive mode, you can run Python code line by line and get immediate feedback instead of running an entire file all at once.  
```
python3 -i file.py
```  

### special need
**add a directory to path**  
step 1: tape the following in the terminal to open the file needed.
```zsh
nano ~/.zshrc
```
step 2:
```zsh
export PATH="${PATH}:<path to directory>"
export PYTHONPATH="${PYTHONPATH}:<path to directory>"
```
step 3: follow the instruction below to exit; save the file and restart the terminal.

### doing assignments
*predicting problems*  
enter the following in the terminal:
```
python3 ok -q <filename> -u
```

*function writing problems*  
writing code in text editor, save it, then open terminal, drop to the required directory, and run ok with this command:
```
python3 ok
```

*debugging using ok*  
open an interactive terminal to investigate a failing test for question.
```
python3 ok -q <question name> -i
```
open an enviroment diagram to investigate a failing test for question.
```
python3 ok -q <question name> --trace
```

## Building Abstractions With Functions
### elements of programming
computer programs consist of instructions to either
- compute some value
- carry out some action
*statements typically describe actions, while expressions typically describe computations.*
In general, statements are not evaluated but executed, while expressions are evaluated but not executed.

every powerful language has three such mechanisms:
- primitive expressions and statements
- means of combination, by which compound elements are built from simpler ones
- means of abstraction, by which compound elements can be named and manipulated as units

types of elements: *functions and data*. Thus, any powerful programming language should be able to describe primitive data and primitive functions, as well as have some methods for combining and abstracting both functions and data.

#### expressions
types of expressions:  
1. primitive expressions: number(2), name(add), string('hello').  
2. compound expressions
   - use infix notation
   - use function notation -- **call expressions**
   ```
   operator(operand, operand)  
   ```
   evaluation procedure:  
   1. Evaluate the operator subexpressions and then the operand subexpressions.  
   2. Apply the function that is the value of the operator to the arguments that are the values of the operands.
   ```
   >>> (lambda: 3)()
   3
   ```
Function notation has three principal advantages over the mathematical convention of infix notation.

#### statements
**assignment statements** -- bound names to value  
execution rule:  
1. Evaluate *all* expressions to the *right* of "=", from left to right. 
2. Bind all names to the left of "=", to those resulting values in the current frame(each name can only be bound to *one* value). 

swapping the values bound to two names can be perfomed in a single statements:
```
y, x = x, y
```
Assignment is the simplest means of abstraction.   

**conditional statements**  
syntax tips:  
1. alwanys starts with "if" clause
2. then zero or more "elif" clauses
3. then zero or one "else" clause. always at the end

only one **kind** of clause may be executed.  
```
>>> def just_in_case():
        x = 10
        if x > 0:
            x += 2
        if x < 13:
            x += 3
        if x % 2 == 1:
            x += 4
        return x
>>>> just_in_case()
19
```     

**conditional expressions**  
```
>>> x = 0
>>> abs(1/x if x!=0 else 0)
0
```

**boolean context**  
- false values: `False`, `0`, `''`, `[]`, `None`
- true values: anything else

- built-in comparison operators(>, <, >=, <=, ==, !=) return boolean values(`True` or `False`).  
- logical operators(*or, and, not*) -- priority from lowest to highest, the last two return the last *value* they evaluate.
```
>>> 1 and 3 and 6 and 10 and 15
>>> 15
>>>
>>> -1 and 1 > 0
>>> True
```

Functions that perform comparisons and return boolean values typically begin with is, not followed by an underscore (e.g., isfinite, isdigit, isinstance).

**iteration**
when there is a infinite loop, press `<control>-c` to force Python to stop looping.

### defining functions 
a function consists of its *signature* and body:
```
def <name>(<formal parameters>):
    return <return expression>
```

execution procedure:  
1. create a function with signature
2. set the body of that function to be everything indented after the first line
3. *bind <name>* to that function in the current frame 

procedure for calling user-defined functions:
1. Add a local frame, forming a new environment
2. bind the function's formal parameters to its arguments *in that frame* 
3. Execute the body of the function in that new environment

bind name to parameter in a local frame; name of funtion vs. function -- `b` vs. `func b(b,x)`.   
```
>>> a = lambda x: x * 2 + 1
>>> def b(b, x):
        return b(x + a(x))
>>> x = 3
>>> b(a, x)
21
```

#### docstring
which must be indented along with the function body. The first line describes the job of the function in one line, followed by a blank line. The following lines can describe arguments and clarify the behavior of the function.

When writing Python programs, include docstrings for all but the simplest functions. Remember, code is written only once, but often read many times. 

#### environments
The possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an environment.

an environment is a sequence of frames.

everytime a defined function is called in the global frame, a new local frame is created.(which means if a function is called *again*, it won't jump to the previous frame but will create a new frame)  

the parent frame of a function is the frame where it was defined, not called.

variable lookup procedure:
1. look in the current frame
2. if not found, recursively look in the parent frame
3. till the global frame, if not found, Error

A *scope* defines the visibility of a name within a block. If a local variable is defined in a function block, the scope *extends to any blocks contained within the defining one*(lexical scope), unless a contained block introduces a different binding for the name -- assignment statements make variables a local variable, which would change it's scope.

a `UnboundLocalError`comes out when executing line A:
```
>>> def f(x):
        def g(y):
            return y + 1     #line A
            x += 1           #line B
        return g
>>> f(2)(3)
```

### designing functions 
- give each function exactly one job. but make it apply to many related situations. 
- don't repeat yourself. implement a process just once, but execute it many times.
- define functions generally. 
  - generalization: find the common stucture among similar related problems, which may be a number, or more likely, a computational process
- gradually forming a habit of coding to make code more **readable and clear**.

#### functional abstractions 
give a name to some computational process, and then referring to that process as a whole without worrying about it's implementation details.  

Understanding functional abstractions via their *domain, range, and intent* is critical to using them correctly in a complex program.

#### pure functions & non-pure functions
- pure functions: just return values  
- non-pure functions: have side effects -- will print sth

Imposing restrictions of pure functions yields substantial benefits.

**return & print**  
- the value that print returns is always None
- the interactive Python interpreter does not automatically print the value None
- no return no value, no print no output
- values and outputs go absolutly different way, one float, one flop
```
>>> x = None
>>> x
>>>


>>> def what_prints():
       print('ok')
       return 'ok'
   
>>>what_prints()
ok
'ok'
```
#### debugging
debugging techniques:  
1. read error messages: from the last line to the first line(upwards).
2. running doctests:
3. writing testing functions
4. using `print` statements
   - add some message to make it easier to read
   ```
   print('debug: tmp was this:', tmp)
   ```
   - long-term debugging
   ```
   debug = True
   def foo(n):
       i = 0
       while i < n:
           i += func(i)
           if debug:
               print('debug: i is', i)
   ```
5. using interactive mode
6. using python tutor
7. using assert statements
   -  An assert statement has an expression in a boolean context, followed by a quoted line of text (single or double quotes are both fine, but be consistent) that will be displayed if the expression evaluates to a false value.
   ``` 
   >>> assert fib(8) == 13, 'the 8th fibonacci number should be 13'
   ```

it's better to crash than to get an incorrect result.

guiding principles of debugging
1. test incrementally
2. isolate errors
3. check your assumptions
4. consult others

**error types**  
`SyntaxError`, `IndentationError`(a tab could be a different number of columns depending on the environment, but a space is always one column. to be consistent, use spaces over tabs!), `TypeError`, `NameError`, `IndexError`.  

`EOL` stands for "end of line".

### higher order function 
a function that manipulates other functions by taking in functions as argument values, returning functions as return values, or both.
```
def cube(k):
    return pow(k, 3)

def summation(n, term):
    """sum the first n terms of a sequence.
    >>>> summation(5, cube)
    225
    """
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total
    
    
def make_adder(n):
    """return a function that takes one argument k and return k + n.
    >>> add_three = make_adder(3)
    >>> add_three(4)
    7
    >>> make_adder(3)(4)
    7
    """
    def adder(k):
        return k + n
    return adder
``` 

Elements with the fewest restrictions are said to have *first-class status*. Python awards functions full first-class status. some of the "rights and privileges" of first-class elements are:
1. They may be bound to names.
2. They may be passed as arguments to functions.
3. They may be returned as the results of functions.
4. They may be included in data structures.

#### self-reference 
return a function using it's own name.
```
def print_sums(n):
    """
    >>> print_sums(1)(3)(5)
    1
    4
    9
    """
    print(n)
    def next_sum(k):
        return print_sums(n + k)
    return next_sum
```

#### currying
transform a multi-argument function into a single-argument, higher-order function.
```
>>> add(2, 3)
5
>>> make_adder(2)(3)
5
```

#### function decorators
apply higher-order functions as part of executing a def statement.
```
>>> def trace(fn):
        def wrapped(x):
            print('->', fn, '(', x, ')')
            return fn(x)
        return wrapped

>>> @trace
    def triple(x):
        return 3 * x
        
>>> triple(12)
-> <function triple at 0x102a39848> ( 12 )
36
```
which is equivalent to :
```
>>> def triple(x):
        return 3 * x
        
>>> triple = trace(triple)
```

decorators are used for tracing, as well as selecting which functions to call when a program is run from the command line.            
    
#### lambda expressions
a function with formal parameter x that returns the value of `x * x`.(a annoymous function -- func λ(x), a shorthand way of writing a def statement)
```
lambda x: x * x
```
bind the function to a name(`square` is not the intrinsic name).
```
square = lambda x: x * x
```

```
>>> x = 10
>>> square = x * x
>>> square
100

>>> square = lambda x: x * x
>>> square(10)
100
>>> (lambda x: x * x)(10)
100

>>> def square(x):
    return x * x
>>> a = square
>>> a(10)
100


>>> b = lambda x: lambda: x
>>> c = b(88)
>>> c
<function <lambda>.<locals>.<lambda> at 0x7ff62e2781f0>
>>> c()
88

>>> def f():
        return 13
>>> (lambda y: y())(f)
13
```

### recursive functions
a function is called recursive if the body of the function calls the function itself, either directly or indirectly. 
```zsh
>>> def fact(n):
        """ 
        n! = n * (n-1) * (n-2)....* 1 -- iteration
        n! = n * (n-1)! -- recursion
        """
        if n == 1:
            return 1
        else:
            return n * fact(n-1)
>>> fact(4)
```
 
recursive function is defined *in terms of itself*, it solves the problem by *simplify* it incrementally, and finally gets to the *edge point*. recursion is an impotant way to think about the nature of computation.  

the **anatomy** of recursive funcitons -- common pattern:  
- def statement header
- conditional statements check for base case(s), the inputs that are simplest to process; a stopping condition for the recursion; the point where we can't reduce the problem any further
- one or more recursive calls, which simplify the original problem  

**recursive leap of faith**
- verify the base case 
- it is often clearer to think about recursive calls as functional abstractions, which is, we should not care about how fact(n-1) is implemented in the body of fact; we should simply trust that it computes (n-1)!; we must *only check that n! is computed correctly if this assumption holds*.

for some reason, recursive functions can be easier to define correctly than iteration.  
recursion approching the oppsite direction as to iteration.  

***practice! practice! practice!***  

#### mutual recursion
When a recursive procedure is divided among two functions that call each other, the functions are said to be mutually recursive. -- call itself indirectly.  
```zsh
>>> def is_even(n):
        if n == 0:
            return True
        else:
            return is_odd(n-1)
            
>>> def is_odd(n):
        if n == 0:
            return False
        else:
            return is_even(n-1)
            
>>> result = is_even(4)
```

Mutually recursive functions can be turned into a single recursive function.  

**printing in recursive functioins**
The computational process evolved by a recursive function can often be visualized using calls to print.
```zsh
>>> def cascade(n):
        """print a cascade of prefixes of n."""
        if n < 10:
            print(n)
        else:
            print(n)
            cascade(n // 10)
            print(n)
>>> cascade(2013)
2013
201
20
2
20
201
2013

>>> def cascade_2(n):
        print(n)
        if n >= 10:
            cascade(n // 10)
            print(n)        
```

#### tree recursion
in which a function calls itself more than once.
```zsh
>>> def fib(n):
       if n == 1:
           return  0
       if n == 2:
           return 1
       else:
       return fib(n-2) + fib(n-1)
       
>>> result = fib(6)           
5
```
This process is highly repetitive: fib is called on the same argument multiple times.  
recursion can be elegant or uneffient.

**Recursive decomposition**: finding simpler instances of problems, exploring differnent possibilities. -- counting partitions

## Building Abstractions With Data
### lists
```zsh
>>> digits = [1, 8, 2, 8]
>>> 
>>> len(digits)                       # the number of elements
>>> 4                 
>>> digits[3]                         # third after the beginning
8                                     
>>> [2, 7] + digits * 2               # concatenation and repetition
[2, 7, 1, 8, 2, 8, 1, 8, 2, 8]
>>> pairs = [[10, 20], [30, 40]]      # nested lists
>>> pairs[1][0]
30
```

## summary(attention！) 
- think procedurally!
- in a program, what most of code's doing are just manipulating names and calling functions. 
- programs must be written for people to read, and only incidentally for machines to execute.

   
         
   
   






