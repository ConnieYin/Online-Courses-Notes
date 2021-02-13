# CS61A
cs61a is a course about managing complexity(mastering abstraction and programming paradigms). it's an introduction to programming(after the class, you can get a full understanding of python fundamentals, combine multiple ideas in large projects, and understand how computers interpret programming languages).
## 目录
1. [intro](#intro)
   1. [doing assignments](#doing-assignments)
   2. [vscode](#vscode)   
   3. [unix commands](#unix-commands)
   4. [python command line options](#python-command-line-options)
2. [functions](#functions)   
   1. [debugging](#debugging)
## intro
computer science is the study of **what** problems can be solved using computation, **how** to solve those problems, and what techniques lead to **effective** solutions.

### doing assignments:
1. predicting problems  
enter the following in the terminal:
```
python3 ok -q <filename> -u
```
2. function writing problems  
writing code in text editor, save it, then open terminal, drop to the lab00 directory, and run ok with this command:
```
python3 ok
```
3. debugging using ok 
open an interactive terminal to investigate a failing test for question.
```
python3 ok -q <question name> -i
```
open an enviroment diagram to investigate a failing test for question.
```
python3 ok -q <question name> --trace
```
### terminology
**terminal**: a program that allows users to enter commands to control the computer.{$(git-bash) or ps(powershell) **VS** command prompt or git-cmd}  
**prompt**: prompt will tell you your current directory:  
```
connie_yin@MacdeMacBook-Air ~ %
```  
**directory**: folder. directories can contain files and directories. (`.`: current directory, `..`: parent directory, `~`: home direcory)  
python interpreter: like python 3  
text editor: like vscode  

### vscode
open vscode in the current working directory via command line:  
```code .
```  
`tab`: indent a line or a group of lines  
`shift-tab`: dedent a line or a group of lines 
`commad-d`: highlights the current word. This allows you to easily rename variables with multiple cursors!  
`command-z`: undo  
`command-shift-z`: redo
`command-s`: save the current file  
 
### unix commands
directories: `ls`, `mkdir`, `cd`(`cd`, `cd ~`, `cd .`, `cd ..`), `rm -r`.  files: `cat`(display), `mv`(move contents or rename), `cp`(copy), `rm`.  
miscellaneous: `echo`(display words on the screen), `man`(displays manual pages for a specified command).  

### python command line options
`-h`: Print a short description of all command line options.  
`-V`: Print the Python version number and exit.  
`-i`: make python to start in interactive mode. In an interactive mode, you can run Python code line by line and get immediate feedback instead of running an entire file all at once.  
```
python3 -i file.py
```  
`-m doctest`: run doctests.  
```
python3 -m doctest file.py
```  
`-v`: display the process of running doctests.
```
python3 -m doctest -v file.py
```
#### special need
add a directory to path:  
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
## functions
### expressions
types of expressions:  
   1. primitive expressions: number(2), name(add), string('hello').  
   2. call expressions: operator(operand, operand){(add(2, 3)}  
      evaluation procedure:  
      1. Evaluate the operator and then the operand subexpressions.(**not execute -- only executed when it's called**)  
      2. Apply the function that is the value of the operator to the arguments that are the values of the operands.
      ```
      >>> (lambda: 3)()
      3
      ```
### assignment statements
execution rule:  
   1. **Evaluate all expressions to the right of "=", from left to right.** 
   2. Bind all names to the left of "=", to those resulting values in the current frame(each name can only be bound to **one** value).  
### defining functions
means of abstraction: binds names to expressions.  
a function consists of it's signature and body.  
execution procedure:  
   1. create a function with signature {<name>(<formal parameters>)}
   2. set the body of that function to be everything indented after the first line(*doesn't execute body!*)
   3. **bind <name> to that function** in the current frame 

procedure for calling user-defined functions:
   1. **Add a local frame**, forming a new environment
   2. Bind the function's formal parameters to its arguments in that frame 
   3. Execute the body of the function in that new environment
```
>>> a = lambda x: x * 2 + 1
>>> def b(b, x):
        return b(x + a(x))
>>> x = 3
>>> b(a, x)
21
```
key point: name of funtion vs. function -- `b` vs. `func b(b,x)`. there is a `b = a`, which bind name b to func a(x), won't change func b(b,x).  

about bulit-in functions:  
when calling built-in functions(like "max"),there is also a process of binding name to function, but we usually don't draw them in the environment diagrams.("max" is just a name, not a function, which means it can be replaced by any other name)  
use functions to avoid repeating code.
### designing functions 
- give each function exactly one job, but make it apply to many related situations. 
- don't repeat yourself: implement a process just once, but execute it many times.
- define functions generally. (generalization: find the common stucture among similar related problems, which may be a number, or more likely, a computational process)
- gradually forming a habit of coding to make code more **readable and clear**.
- functional abstractions: give a name to some computational process, and then referring to that process as a whole without worrying about it's implementation details.  
   what dose sum_squares need to konw about square in order to use it correctly?
   - square takes one argument
   - square computes the square of a number
   ```
   def square(x):
       return mul(x, x)

   def sum_squares(x, y)
       return square(x) + square(y)
   ```

functions are first-class: functions can be manipulated as values.  
**higher-order function: a function that manipulates other functions by taking in functions as argument values, returning functions as return values, or both.**
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
```
```
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
make_adder(3)(4) indicates operator of a call expression can also be a call expression.  

sometimes, functions may look complex. just think a function as a whole, conclude it's function. 
**application**  
self-reference: return a function using it's own name.
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
function currying: transform a multi-argument function into a single-argument, higher-order function.
```
>>> add(2, 3)
5
>>> make_adder(2)(3)
5
```
**lambda expressions: expressions that evaluated to functions.**  
`lambda x: x * x`: a function with *formal parameter x* that *returns* the value of "x * x".(a annoymous function -- func λ(x), a shorthand way of writing a def statement -- **see it as f** -- the return expression is not evaluated until the lambda is called. This is similar to how defining a new function using a def statement does not execute the function’s body until it is later called)  
`square = lambda x: x * x`: bind the function to a name(but `square` is not the intrinsic name).(vs. def statement, when is better to use lambda than def statement)
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

### environment diagrams
the current environment is either:  
   - the global frame alone, or
   - a local frame, followed by the global frame
**an environment is a sequence of frames**.  
everytime a defined function is called in the global frame, a new local frame is created.(which means if a function is called *again*, it won't jump to the previous frame but will create a new frame)  
the parent frame of a function is the frame where it was defined, not called.

## control
### none
- **a function that does not explicitly return a value will return None**
- None is not displayed by the interpreter as the value of an expression
```
>>> x = None
>>> x
>>>
```
### return vs print
**no return no *value*, no print no *output*.**  
**values and outputs go absolutly different way, one float, one flop.**
```
>>> a = hailstone(10)
10
5
16
8
4
2
1
>>> a
7
```
pure functions: just return values  
non-pure functions: have side effects(will print, thus will display sth, but it's not its value).  
```
def what_prints():
   print('hello world')
   return 'hello world'
   print('cs61a is awesome')
   
>>>what_prints()
hello world
'hello world'
```
### conditional statements
only one **kind** of clause may be executed.  
take care! when you dicide to write *more than one* if or elif.
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
syntax tips:  
   1. alwanys starts with "if" clause
   2. then zero or more "elif" clauses
   3. then zero or one "else" clause. always at the end

conditional expressions:
```
>>> x = 0
>>> abs(1/x if x!=0 else 0)
0
```
**operators**
- built-in comparison operators: return boolean values(Ture or False).  
- logical operators(`or`, `and`, `not` -- priority from lowest to highest): return the last *value* they evaluate.
    - false values: `False`, `0`, `''`, `[]`, `None`
    - true values: anything else
```
>>> 1 and 3 and 6 and 10 and 15
>>> 15
>>>
>>> -1 and 1 > 0
>>> True
```
### debugging
#### debugging techniques:  
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
      (it's better to crash than to get an incorrect result)
#### error types
`SyntaxError`, `IndentationError`(a tab could be a different number of columns depending on the environment, but a space is always one column. to be consistent, use spaces over tabs!), `TypeError`, `NameError`, `IndexError`.  
`EOL` stands for "end of line".
## summary(attention) 
- a function will be executed only when it's called.
- lambda expressions is actually f, until it's called.
- in a program, what most of code's doing are just manipulating names and calling functions. 


   
         
   
   






