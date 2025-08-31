# CS50 Week 2 — Arrays

## Compiling Programs

- **Basic compilation**

  ```bash
  make hello
  # or
  clang hello.c
  ./a.out
  ```

- **Custom output name**

  ```bash
  clang -o hello hello.c
  ./hello
  ```

- **With CS50 library**

  ```bash
  clang -o hello hello.c -lcs50
  ./hello
  ```

## Debugging

- **Classic way**
  Use `printf` statements to inspect values while running your program.

- **CS50 debugger**

  ```bash
  debug50 ./buggy
  ```

  - **Breakpoints**: stop the program at specific lines to check variables.
  - **Step into**: goes inside a function’s implementation.
  - **Garbage value**: leftover memory from previous programs.

## The Compilation Process

1. **Preprocessing** → Preprocessor handles directives (e.g., `#include`), essentially copy-pasting headers and macros into your code.
2. **Compiling** → Converts C code into assembly code.
3. **Assembling** → Converts assembly code into machine-readable binary.
4. **Linking** → Combines your program with external libraries (e.g., CS50 library, standard libraries) so function calls are resolved.

⚠️ **Reverse Engineering**: Some compilation steps can be reversed (like decompiling binaries), but as programs grow complex, reversing becomes tedious and incomplete.

## Arrays

- Arrays are **sequences of values stored back-to-back in memory**, all of the same data type.
- Strings in C are **arrays of characters**, always ending with an extra byte: `'\0'` (NUL).
- Example:

  ```c
  words[0][0];  // Strings can be thought of as 2D arrays
  ```

## Useful Libraries & Functions

- `ctype.h`

  - `toupper();` → Convert characters to uppercase.

- `string.h`

  - `strlen();` → Get the length of a string.

- **Manual pages**: [manual.cs50.io](https://manual.cs50.io)

## Exit Status

- `exit(0)` → Program finished without errors.
- Any non-zero number → Indicates an error (e.g., `1`, `404`, `1511`).

## Command-Line Arguments

```c
int main(int argc, string argv[]);
```

- `argc`: argument count.
- `argv[]`: array of strings (the arguments).

## Fun with ASCII Art

**Cowsay**

```bash
cowsay hello
cowsay -f duck quack
cowsay -f dragon rawr
```

## Cryptography (Basics)

```
Key        -> Used to encrypt/decrypt
Plaintext  -> Original readable message
Ciphertext -> Encrypted message
```

```
plaintext + key = ciphertext
```
