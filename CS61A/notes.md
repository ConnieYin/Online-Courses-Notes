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
1.predicting problems  
enter the following in the terminal:
```
python3 ok -q <filename> -u
```
2.function writing problems  
writing code in text editor, save it, then open terminal, drop to the lab00 directory, and run ok with this command:
```
python3 ok
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



when using the `ok` autograder.
```zsh
python3 ok -q sum_digits -i
```
to open an interactive terminal to investigate a failing test for question sum_digits.

```zsh
python3 ok -q sum_digits --trace
```
to look at an enviroment diagram to investigate a failing test for question sum_digits.

to add a directory to path:

open the terminal and tape the following to open the file:
```zsh
nano ~/.zshrc
```
then tape the following: 
```zsh
export PATH="${PATH}:<path to directory>"
export PYTHONPATH="${PYTHONPATH}:<path to directory>"
```
last, follow the instruction below to exit; save the file and restart the terminal.




## functions
### expressions
types of expressions:  
   1. primitive expressions: number(2), name(add), string('hello').  
   2. call expressions: operator(operand, operand){(add(2, 3)}  
      evaluation procedure:  
      1. Evaluate the operator and then the operand subexpressions.  
      2. Apply the function that is the value of the operator to the arguments that are the values of the operands.
### assignment statements
execution rule:  
   1. **Evaluate** all expressions to the right of "=", from left to right. 
   2. **Bind** all names to the left of "=", to those resulting values in the current frame(each name can only be bound to **one** value).  
### defining functions
means of abstraction: binds names to expressions.  
a function consists of it's signature and body.  
execution procedure:  
   1. create a function with signature {<name>(<formal parameters>)}
   2. Set the body of that function to be everything indented after the first line.
   3. Bind <name> to that function in the current frame.

### debugging
debugging techniques:

running doctests:

```zsh
python3 -m doctest file.py
```
`-v` option stands for *verbose*.In addition to telling you which doctests you failed, it can also tell you which doctests passed.
```zsh
python3 -m doctest file.py -v
```



