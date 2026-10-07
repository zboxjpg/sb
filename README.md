# SimpleBuilder
**SimpleBuilder** is simple python library which I made for myself to provide simple building operations *(and not use .sh/.bat files)*.

# Installation
```bash
pip install sbuilder
```

# Examples
## Running an OS specific command
```py
from sbuilder import *

platform = GetPlatform()
cmd = ""

if platform == Platform.WIN32:
    cmd = "python"
else:
    cmd = "python3"

b = Builder()
t = Task(cmd)
t.AddArgs("-v", "main.py")
b.AddTask(t)
b.CMDRun()
```

## Working with `Status`
```py
from sbuilder import *

t_compile = Task("gcc")
t_compile.AddArgs("main", "-o", "src/main.c")

t_run = Task("./main")

b = Builder()
b.AddTask(t_compile)

if b.CMDRun() == Status.OK:
    b.ClearTasks()
    b.AddTask(t_run)
    b.CMDRun()
```

# Documentation

## Functions
func `GetPlatform()` - get system platform

| System                         | Value             |
|--------------------------------|-------------------|
| Linux                          | Platform.LINUX    |
| Windows                        | Platform.WIN32    |
| Windows/Cygwin                 | Platform.CYGWIN   |
| Windows/MSYS2<br>Windows/MinGW | Platform.MSYS     |
| Mac OS X                       | Platform.MACOSX   |
| OS/2                           | Platform.OS2      |
| OS/2 EMX                       | Platform.OS2EMX   |
| RiscOS                         | Platform.RISCOS   |
| AtheOS                         | Platform.ATHEOS   |
| FreeBSD 6                      | Platform.FREEBSD6 |
| FreeBSD 7                      | Platform.FREEBSD7 |
| FreeBSD 8                      | Platform.FREEBSD8 |
| FreeBSD N                      | Platform.FREEBSDN |

## class `Task(cmd, com)`
- param `cmd` - command to run (e.g. "python", "gcc", etc.)
- param `com` - print comment instead of standard log

func `AddArgs(args)` - add arg to task (e.g. `.AddArgs("main.c", "-o", "app")`). This is a fluent method that returns the instance itself for chaining.

func `GetFullTask()` - return task as list (e.g. `.GetFullTask()` will return `['gcc', 'main.c', '-o', './app']`)

## class `Builder()`
func `AddTask(task)` - add task to builder. This is a fluent method that returns the instance itself for chaining.

func `ClearTasks()` - remove all tasks. This is a fluent method that returns the instance itself for chaining.

func `CMDRun()` - run tasks synchronously. This is a fluent method that returns the instance itself for chaining.
