# CS61A
## 目录
1. [getting started](#getting-started)   
   1. [vscode](#vscode)   
   2. [unix commands](#unix-commands)
   3. [useful python command-line options](#useful-python-command-line-options)
2. [functions](#functions)   
   1. [debugging](#debugging)
## getting started
### vscode
open the command palette: `command` + `shift` + `p`   
save the current file: `command` + `s`   
dedent: `shift` + `tab`   
 
### unix commands
terminal: $(git-bash) or ps(powershell) VS command prompt or git-cmd

common terminal commands: `ls`, `cd` (`cd ..`, `cd ~` and `cd`), `mkdir`, `mv`， `rm -r`, 


### useful python command-line options
```zsh
python3 -i file.py
```
`-i` --make python to start in interactive mode. In an interactive mode, you can run Python code line by line and get immediate feedback instead of running an entire file all at once.

```zsh
python3 -m doctest file.py
```
`-m doctest` --to run doctests.

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

when using the `ok` autograder.
```zsh
python3 ok -q sum_digits -i
```
to open an interactive terminal to investigate a failing test for question sum_digits.

```zsh
python3 ok -q sum_digits --trace
```
to look at an enviroment diagram to investigate a failing test for question sum_digits.


## functions

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



