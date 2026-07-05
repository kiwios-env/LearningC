# Notes That I Do Not Already Know

## More about gcc

- Run `gcc`:
```bash
kiwi% gcc -Wall infilename.c -o outfilename.o
```
- `-Wall` enables most compiler warnings
- More complicated forms exist
  - multiple source files
  - auxiliary directories
  - optimization, linking
- Embed debugging info and disable optimization
```bash
kiwi% gcc -g -O0 -Wall infilename.c -o outfilename.o
```

## Debugging

- `gdb` or "GNU Debugger" is commonly used to debug C and ASM programs
- Some useful commands:
  - `break *linenumber*` - create breakpoint at specified line
  - `break file:*linenumber*` - create breakpoint at line in file
  - `run` - run program
  - `c` - continue execution
  - `next` - execute next line
  - `step` - execute next line or step into function'
  - `quit` - quit `gdb`
  - `print *expression*` - print current value of the specified expression
  - `help *command*` - in-program help
- Can use `valgrind` for memory debugging

## More about header files

- Included files must be on *include* path
  - `-I*directory*` with `gcc`: specify additional include directories
  - standard include directories assumed by default

## Order of Operations

| **Operator**  | **Evaluation direction**  |
|---|---|
| `+`, `-` (sign) | right-to-left  |
| `*`, `/`, `%`  | left-to-right  |
| `=`, `+=`, `-=`, `*=`, `/=`, `%=`  | right-to-left  |
| `+`, `-`  | left-to-right  |

- Use parentheses to override order of evaluation

## Function Prototypes

- Functions must be declared before use, called a *function prototype*
- Examples:
```c
int factorial(int);

int factorial(int n);
```
- General form:
  - `return_type function_name(arg1,arg2,...);`

## Function Definitions

- Must match prototype if there is one
- No semicolon at end
- Curly braces define a region of code
- Variable declarations before other statements

## Console I/O

- `stdio`, `stdin`: console output and input streams
- `puts(string)`: print string to stdout
- `putchar(char)`: print character to stdout
- `char = getchar()`: return character from stdin
- `string = gets(string)`: read line from stdin into string

## Defining Expression Macros

- `#define` can take arguments and be treated like a function
  - `#define add3(x,y,z) ((x)+(y)+(z))`
- parentheses ensure order of operations
- compiler performs inline replacement; not suitable for recursion

## Conditional Preprocessor Macros

- `#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, `#endif`
- conditional preprocessor macros can control which lines are compiled
  - evaluated before code itself is compiled, so conditions must be preprocessor defines or literals
  - the `gcc` option `-Dname=value` sets a preprocessor define that can be used
  - Used in header files to ensure declarations happen only once
- `#pragma`: preprocessor directive
- `#error`, `#warning`: trigger a custom compiler error/warning
- `#undef` msg: remove the definition of `msg` at compile time

## Compiling Our Code:
```bash
kiwi% gcc -g -O0 -Wall hello.c -o hello.o
kiwi% gdb hello.o
...
Reading symbols from hello.o...done.
(gdb) run
Starting program: hello.o
hello, 6.087 students
Program exited normally.
(gdb) quit
kiwi%
```