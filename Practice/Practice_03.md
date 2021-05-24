Safety Management, Practice #3
==============================

## Problem #1: "Switch and Branch Table"

Write a program `08` to print the season's name (Winter, Spring, Summer, or
Fall) for a given month number (from 1 to 12). For any number outside of the
range from 1 to 12, the program should print the message "Invalid month number."
Write a version of a program (`08.c`) with a multi-way `if` construct. Use
logical operators inside the `if` conditions. Compile the program and analyze
its assembly with Radare2 in graph mode. Rewrite the source file replacing the
`if` construct and logical operators with a `switch` construct. Compile and
analyze the binary with Radare2. Compare and contrast the generated code with
the `if` assembly version.

Rewrite your program by only using a one-way if construct and the `goto`
statement to jump in the code's flow to various labels similar to how the
assembly was structured in R2 for the `switch` construct. The source file should
be named `08.goto.c`. Rewrite the `switch` construct in x86-64 inline assembly
in `08.inline.c`.

## Problem #2: "Swap"

Write a program `09` to swap two numbers in a function called `swap`. Write
an incorrect version first (without the use of pointers). Check out the
assembly in the [Godbolt Compiler Explorer](https://godbolt.org) with the
`-O3` flag. Write a correct working version. Compare the new assembly to
the previous one. Try adding the `-fno-inline` in Godbolt. Compare the
assembly again.

## Problem #3: "Array Sum"

Write a program `10` to find a sum of an array of random integers. Create two
functions named `fill_with_random` and `sum` that can prepare and sum the array.
Create the array on the heap with the `malloc` function. Do not forget to
release the memory with the `free` function. Check out the assembly in the
[Godbolt Compiler Explorer](https://godbolt.org).

Write a program `11` to find a sum of all the numbers passed as command-line
arguments to the program. Convert the strings to integers with the `strtol`
function. Check out the assembly in the [Godbolt Compiler Explorer](https://godbolt.org).

## Problem #4: "Safer World of C++"

Copy the main source file of the `09` Swap program (`09.c`) to the new
`problem-04` directory under the name `12.cpp`. Do the same for the `10.c` file.
Save it under the name `13.cpp`. Compile two programs with the GNU C++ compiler.
Modify the code of the program `13` to fix the compilation error as it was done
during the class. Notice how the C code can still be compiled with the C++
compiler without or with just minor modifications. Rewrite as much C code as
possible to the appropriate safer C++ code constructs. Ensure the final versions
of your programs can be compiled and still produce the same results as their C
counterparts.

## Problem #5: "Classes and Objects"

Follow the instructor to create a simple `rational` class in C++ in files
`rational.h` and `rational.cpp`. Write a simple test program `14.cpp` to sum any
two arbitrary numbers and print the result. Finish overloading the `-=`, `-`,
`*=`, `*`, `/=`, `/` operators. Put your code into the [Godbolt Compiler
Explorer](https://godbolt.org). Take a look at the assembly generated with the
`-O1` optimization flag by the x86-64 GCC 11.1 compiler. Find the call to the
constructor of the first number (you will see something like `call
rational::rational(int, int)...` in the assembly output for the `main`
function). Find how the numerator and denominator are passed as a second and
third arguments through registers `esi`/`rsi` and `edx`/`rdx`. Something else is
passed as a first argument to the constructor through the register `edi`/`rdi`
that we were not sending in our high-level code. Find out what it is. You can
use books and the Internet in your research. Provide the answer at the end of
your video.

## GitHub Checkpoint #3, Part 1-5

For the third GitHub Checkpoint, you need to prepare, commit, and push Problem
1 through 5 to your private course repository on GitHub. You have to get the
repository from the instructor if you don't have one. Submit the last commit ID
without any extra characters to Canvas, pointing to the snapshot where all the
code is ready. You may create new commits and resubmit before the deadline
multiple times.

You must also record your work with the server for the lab problems. You can use
Zoom to record the sessions to the disk. The recordings must be concise and must
have your commentaries explaining the most important steps of the process. Do
the operations that the instructor was doing. You may pretend that you are an
instructor now, and you are trying to create a series of educational videos. You
have to upload them to the AUCA Google Drive folder (create one, name it
appropriately) and share them with the instructor (you can find his E-mail in
the course syllabus). DO NOT remove the videos until the end of the course. If
it is not possible to download or watch the video, you will get zero for the
work. Recording URLs (and nothing else) must be stored in `rec.txt` files for
every problem. [Here](https://drive.google.com/file/d/1Q_jFnOCQbJGYS1Ky8rfQ-F389PVioOYV)
you can find the video that shows how to record, upload, share, and get the URL
to write to `rec.txt`.

Here is the list of things that you MUST present in the video for Problem 1.

1. Connect to the server.
2. Write the program `08.c` with the `if` construct and logical operators.
3. Take a look at the assembly in R2. Analyze how it is structured.
4. Rewrite the program `08.c`. Use the `switch` construct this time.
5. Take a look at the assembly in R2. Analyze how it is structured. Compare and
   contrast the code to the one with the `if` construct.
6. Try to rewrite your program by only using a one-way if construct and
   the `goto` statement to jump in the code's flow to various labels similar
   to how the assembly was structured in R2 for the `switch` version of code.
   Name the source files `08.goto.c`. Compile and test your program.
7. Rewrite the `switch` part of the code in 64-bit x86 inline assembly as it was
   done during the class. Name the source files `08.inline.c`. Compile and test
   it.
8. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 2.

1. Connect to the server.
2. Write the C program `09.c` to swap two numbers in a function called `swap`.
   Write an incorrect version first (without the use of pointers). Check out the
   assembly in the [Godbolt Compiler Explorer](https://godbolt.org) with the
   `-O3` flag. Explain the the reason the program is not correct.
3. Write a correct working version by using pointers. Compare the new assembly
   to the previous one in Godbolt CE. Try adding the `-fno-inline` in Godbolt.
   Compare the assembly again. Explain the results.
4. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 3.

1. Connect to the server.
2. Write the C program `10.c` to find a sum of an array of random integers.
   Ensure to create the array on the heap.
3. Explain the difference between the heap and the stack.
4. Check out the assembly in the [Godbolt Compiler Explorer](https://godbolt.org).
5. Explain what information is necessary to access an element of an array in the
   low-level world. Point out in what lines of assembly our array is being used.
6. Write the C program `11.c` to find a sum of all the numbers passed as
   command-line arguments to the program. Explain what is stored as the first
   element of the `argv` array in the world of C and C++.
7. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 4.

1. Connect to the server.
2. Copy `09.c` to the new `problem-04` directory under the name `12.cpp`.
3. Do the same for the `10.c` file. Save it under the name `13.cpp`.
4. Compile both programs and get the executables to run. Run the code. Ensure
   the results are correct.
5. Rewrite as much C code as possible to the appropriate safer C++ code. Ensure
   the final versions of your programs can be compiled and still produce the
   same results as their C counterparts.
6. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 5.

1. Connect to the server.
2. Create a simple `rational` class in C++ in files `rational.h` and
   `rational.cpp`. Write a simple test program `14.cpp` to sum any
   two arbitrary numbers and print the result. Finish overloading the `-=`, `-`,
   `*=`, `*`, `/=`, `/` operators. Compile and run your program. Ensure that
   it produces a correct result.
3. Put your code into the [Godbolt Compiler Explorer](https://godbolt.org). Take
   a look at the assembly generated with the `-O1` optimization flag by the
   x86-64 GCC 11.1 compiler. Find the answer to the question specified in the
   description of Problem #5.
4. Disconnect from the server.

Here is the directory structure with the names of the files that you must use.

```
<Your private GitHub repository>
├── ...
├── lab-03
│   ├── problem-01
│   │   ├── 08.c
│   │   ├── 08.goto.c
│   │   ├── 08.inline.c
│   │   └── rec.txt
│   ├── problem-02
│   │   ├── 09.c
│   │   └── rec.txt
│   ├── problem-03
│   │   ├── 10.c
│   │   ├── 11.c
│   │   └── rec.txt
│   ├── problem-04
│   │   ├── 12.cpp
│   │   ├── 13.cpp
│   │   └── rec.txt
│   └── problem-05
│       ├── 14.cpp
│       ├── rational.cpp
│       ├── rational.h
│       └── rec.txt
└── Readme.md
```

Here you can find the commands that will be used to compile your code.

| Problem             | Compilation Commands                                                                                                    |
| :------------------ | :---------------------------------------------------------------------------------------------------------------------- |
| p01: 08.c...        | `gcc -g -fno-stack-protector -o 08 08.c` and `gcc -o 08 08.goto.c` and `gcc -static -fno-pie -no-pie -o 08 08.inline.c` |
| p02: 09.c           | `gcc -O3 -fno-inline -o 09 09.c`                                                                                        |
| p03: 10.c, 11.c     | `gcc -o 10 10.c` and `gcc -o 11 11.c`                                                                                   |
| p04: 12.cpp, 13.cpp | `g++ -o 12 12.cpp` and `g++ -o 13 13.cpp`                                                                               |
| p05: 14.cpp...      | `g++ -c -o rational.o rational.cpp && g++ -c -o 14.o 14.cpp && g++ -o 14 rational.o 14.o`                               |

Ensure NOT to submit any binary files (object files and executables). Your grade
will be lowered for that. You will get zero for a late submission. You will get
zero if the auto-grading script cannot parse your commit, clone your repository,
check out the commit, find your source files under the specific names the
instructor was using during the class, build the sources, run your programs. You
will also get zero if your programs' output format is not the same as that
outlined in the samples.

### Documentation

    man make
    man gcc
    man as
    man gdb
    man objdump

### Links

#### C

* [Beej's Guide to C Programming](https://beej.us/guide/bgc)

#### x86 ISA

* [Intel® 64 and IA-32 Architectures Software Developer Manuals](https://software.intel.com/en-us/articles/intel-sdm)
* [X86 Opcode Reference](http://ref.x86asm.net/index.html)
* [X86 Instruction Reference](http://www.felixcloutier.com/x86)
* [Intel x86 JUMP Quick Reference](http://www.unixwiz.net/techtips/x86-jumps.html)
* [Optimizing subroutines in assembly language](https://www.agner.org/optimize/optimizing_assembly.pdf)

#### Tools

* [Pro Git](https://git-scm.com/book/en/v2)
* [GAS Syntax](https://en.wikibooks.org/wiki/X86_Assembly/GAS_Syntax)
* [GDB Quick Reference](https://users.ece.utexas.edu/~adnan/gdb-refcard.pdf)
* [inline GCC](https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html)
* [The Official Radare2 Book](https://book.rada.re)

### Books

#### C

* C Programming: A Modern Approach, 2nd Edition by K. N. King
* C Programming Language, 2nd Edition by Brian W. Kernighan and Dennis M. Ritchie
