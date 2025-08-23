# CS50 Week 1: C

## Compilation flow

`Source code → [Compiler] → Machine code`

- Editor: **Visual Studio Code for CS50** → [https://cs50.dev](https://cs50.dev)
- Manual pages: **CS50 Manual** → [https://manual.cs50.io](https://manual.cs50.io)

---

## Interfaces

- GUI: Visual Studio Code
- CLI: Command Line Interface (terminal)

---

## Create, compile, run

```bash
code hello.c     # create or open a file
make hello       # compile
./hello          # run the program
ls               # list files in the current directory
clear            # clear the terminal
```

### Minimal program

```c
#include <stdio.h>

int main(void) {
    printf("hello, world\n");
}
```

> `hello*` in `ls` output means the file is executable.

---

## Common CLI commands

- `cd` move to a directory
- `cp` copy a file
- `mkdir` create a directory
- `mv` move or rename a file
- `rm` remove a file
- `rmdir` remove an empty directory

---

## CS50 library (`cs50.h`) input helpers

- `get_char`
- `get_double`
- `get_float`
- `get_int`
- `get_long`
- `get_string`

Example:

```c
#include <cs50.h>
#include <stdio.h>

int main(void) {
    string answer = get_string("What's your name? ");
    printf("Hello, %s!\n", answer);
}
```

---

## Escape sequences

- `\n` newline
- `\r` carriage return (moves cursor to the start of the line)

---

## Functions and arguments

- Arguments are values you pass into functions.
- Functions can produce side effects (for example, printing to the screen).

```c
#include <stdio.h>

void meow(void) {             // no arguments
    printf("meow\n");
}

void meow_n(int n) {          // with an argument
    for (int i = 0; i < n; i++) {
        printf("meow\n");
    }
}
```

> Note: C does not support function overloading. Use different function names if you want different parameter lists.

---

## Data types and `printf` formats

| Type     | Format                      |
| -------- | --------------------------- |
| `bool`   | `%i` (prints 0 or 1)        |
| `char`   | `%c`                        |
| `double` | `%f` (or `%lf` for `scanf`) |
| `float`  | `%f`                        |
| `int`    | `%i`                        |
| `long`   | `%li`                       |
| `string` | `%s`                        |

---

## Conditionals

```c
if (x < y) {
    // do something
}

if (x < y) {
    // do something
} else {
    // otherwise do this
}
```

---

## Operators

**Assignment**

- `=`

**Arithmetic**

- `+`, `-`, `/`, `%`

**Comparison**

- `==`, `!=`, `<`, `>`, `<=`, `>=`

---

## Variables, constants, and style

- Declare variables with an appropriate type.
- Use constants for fixed values:

```c
const int DAYS_IN_WEEK = 7;
```

- Aim for correctness, good design, and clear style.

---

## Pitfalls to remember

- **Floating point imprecision**: decimal math with `float` or `double` can have rounding errors.
- **Integer overflow**: values that exceed the range of an integer wrap around.

---

## Quick reference

### Commands

| Task                   | Command          |
| ---------------------- | ---------------- |
| Create or open a file  | `code hello.c`   |
| Compile                | `make hello`     |
| Run                    | `./hello`        |
| List files             | `ls`             |
| Clear terminal         | `clear`          |
| Change directory       | `cd <dir>`       |
| Copy file              | `cp <src> <dst>` |
| Move or rename         | `mv <src> <dst>` |
| Make directory         | `mkdir <dir>`    |
| Remove file            | `rm <file>`      |
| Remove empty directory | `rmdir <dir>`    |

### Cheats

- `#include <stdio.h>` brings in standard I/O functions like `printf`.
- `#include <cs50.h>` enables `get_*` input helpers.
- Executable files often appear with a trailing `*` in `ls`.
