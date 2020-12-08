# Online Courses Notes
## 目录
1. [The Missing Semester of Your CS Education](#the-missing-semester-of-your-cs-education) 
    1. [course overview + the shell](#course-overview--the-shell)
2. [CS61A](#cs61a)
    1. [getting started](#getting-started)
## The Missing Semester of Your CS Education
### course overview + the shell
#### what is the shell?
> To take full advantage of the tools your computer provides, we have to go old-school and drop down to a textual interface:The Shell.  

> They allows you to run programs, give them input, and inspect their output in a semi-structured way.  

> We will focus on the Bourne Again Shell, or "bash" for short.  
#### using the shell
```bash
connie_yin@MacdeMacBook-Air ~ %
```
`~`is short for home directory; `%`means you are not the root user.

```bash
connie_yin@MacdeMacBook-Air ~ % date
2020年12月 8日 星期二 12时31分40秒 CST
```

```bash
connie_yin@MacdeMacBook-Air ~ % echo hello
hello
```
the shell parses the command by splitting it by whitespace. the first word is parsed as a program(`date`, `echo`); the subsequent word is parsed as an argument that the program can access(the `echo`program simply prints out its argument - `hello`).

if you want to provide an argument that contains spaces or other special characters, you can either quote the argument with `'` or `"`(e.g.,`'my photos'`), or escape just the relevant character with `\`(`my\photos`).

```bash
connie_yin@MacdeMacBook-Air ~ % echo $path
/usr/local/sbin /usr/local/bin /Library/Frameworks/Python.framework/Versions/3.8/bin /usr/local/bin /usr/bin /bin /usr/sbin /sbin /Library/TeX/texbin
```

```bash
connie_yin@MacdeMacBook-Air ~ % which date
/bin/date
```
`$path` is a environment variable that lists which directories the shell should search for programs when it is given a command. 

$ symbol indicating bash


## CS61A
### getting started
要注意常用python command line options

