Safety Management, Practice
===========================

In this course, we study the influence of the C and C++ programming languages on
the modern world. The reason is that C and C++ were and still are the
irreplaceable technologies that are used to build fundamental software such as
Operating System kernels, hardware drivers, and high-performance software such
as browsers that we use every day. In the beginning, we study the fundamental
structured and object-oriented programming elements of the languages. Next, we
explore how those languages' design decisions influence the world from the point
of safety and what extra cost people have to bear for some of the unique
features.

## Developer Tools

The following tool is required to be installed to work on this course. It
contains the Git version control system that you will use to submit your work to
the instructor. The Git installation package also includes a virtual terminal
Mintty, the command interpreter Bash, and an SSH client to connect and work
with the course server.

* [Git SCM](https://git-scm.com)

On macOS, it is recommended to install the official command-line developer
tools from Apple by opening the `Terminal.app` and running the following
command.

```bash
xcode-select --install
```

The following code editor is optional. It is not required, but it can be helpful
if you will not feel comfortable working with the command-line interface for
long periods. You have to install the 'Remote - SSH' extension from the editor
to use it with our remote server.

* [Microsoft Visual Studio Code](https://code.visualstudio.com)

This virtualization software and the OS images will allow you to set up your
development environment on your computer to not depend on the course server. It
is optional to set it up. You are on your own here as we will not help you
figure out what to do to get your environment up and running. Internet is full
of information about the process, though.

* [Oracle VM VirtualBox](https://www.virtualbox.org)
* [Ubuntu 20.04 Desktop](https://ubuntu.com/#download) with GUI or the
  [server](https://ubuntu.com/download/server) version without it

## Development Environment

To setup, a development environment, open the terminal (for example, through
`git-bash` on Windows) and run the Secure Copy (`scp`) program to download
credentials to your machine to login to the course server. Your credentials will
include public and private RSA cryptographic keys with a configuration file to
point to our server with your login information. To download the keys, you will
have to agree with any prompts by typing `yes` and pressing enter. You will also
have to type the password when prompted. The password will be given to you
during the class. The passwords will be disabled two weeks after the start of
the course. Ensure to get your keys before that. You will not be able to see
your password when you type it. It is normal not to leak it to your command-line
history file or show it to people nearby. Continue typing the password. If the
system does not accept your password multiple times, type it into a text editor,
cut and paste it into the terminal window. Remember that `CTRL+C` and `CTRL+V`
key combinations do not work in most Unix terminals. You will have to use other
key combinations that are different for different terminals. Mintty on Windows
uses `CTRL+INSERT` and `SHIFT+INSERT` by default. macOS terminal users are
luckier as they can use the standard `COMMAND+C` and `COMMAND+V` key
combinations.

```bash
# WARNING: If you have existing .ssh keys or configuration files, make a backup of them first.
scp -r <AUCA login>@auca.space:~/.ssh ~/
```

Do not forget to replace `<AUCA login>`, including the `<` and `>` character,
with your actual AUCA login. For example, `toksaitov_d` would be the text the
instructor of this course would write to download the keys to access the server.

From now on, you can access the server with all the necessary tools installed by
issuing the following command in your terminal.

```bash
ssh auca
```

To terminate the connection from the remote server, you can issue the `exit`
command.

It is a good idea to create a separate directory for the course work on the
server and give it a meaningful name (e.g., `com-121`). You should probably
keep different labs (experiments) in separate directories, too. Name them
appropriately. Use the commands and programs such as `cd`, `mkdir`, `mv`,
`touch`, `nano`, `cat`, `man`, and `ls`. 

## Problem #1: "Portability, Inline Assembly"

Write a program in C that reads one uppercase Latin letter from the user through
the `getchar` function, converts it to a lowercase letter, and prints it to the
screen, followed by a newline `\n` sequence with a `putchar` function. Read the
docs about `getchar` and `putchar` first with the `man` command.

Compile the program to the assembly file under the name `04.x86-64.s`. Next,
compile the program with a flag `-m32` into assembly under the name `04.x86.s`.
Do the same, but with another compiler, `aarch64-linux-gnu-gcc`. Save the last
assembly file under the name `04.aarch64.s`. All of these files are compiled for
different CPU Instruction Set Architectures (ISA). The assembly for every ISA
should also be different. Try to observe that. Now, repeat the process, but
finish compiling into executable machine files `04.x86-64`, `04.x86`, and
`04.aarch64`. With `objdump` and `aarch64-linux-gnu-objdump` programs, observe
if the machine code for the `main` function is the same. Try to run the programs.
Try to answer why it is possible or impossible to do that.

Create a `04.inline-x86.c` file. Copy all the code from the `04.c` program.
Use the [inline GCC](https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html) x86
assembly to do the conversion from uppercase to lowercase directly in a C file.
In your assembly, you should put the input value to the `al` register, add a
certain number to switch it to uppercase according to the [ASCII table](https://en.wikipedia.org/wiki/ASCII#Printable_characters),
write the value to the output variable used by the compiler. You should
connect the C and assembly world by specifying input constraints and outlining
corrupted (clobbered) registers (in our case, just `eax`). Compile, run, and
step through your assembly instructions one by one in `gdb`. Use additional
`-m32 -masm=intel` flags to compile your program. `-m32` option will tell the
compiler to use the older x86 ISA (which we can still use on new x86-64 CPUs).
`-masm-intel` option will allow us to use an objectively nicer syntax for x86
assembly which is popular in various assembly books and is the official syntax
used by Intel in their documentation files. Note that GNU programs (GCC, AS,
GDB) prefer the AT&T syntax, which has reverse operand order and requires a lot
of punctuation-noise in assembly sources.

## Problem #2: "Selection Constructs"

Write a program `05` to read one character from the user. Compare the character
with ' ' and '\t' (tab) values to check that it is a whitespace symbol to set a
boolean variable (name it appropriately). For educational purposes, use a
multiway `if` selections constructs and nothing else. At the end of the
program, use a two-way if construct to check the boolean value to display
"Whitespace" or "Not a whitespace" messages to the user. Generate preprocessor
output `05.i`, find out the "true" (pun intended) nature of boolean values in C.
Take a look at the assembly in GDB. Step through the code to analyze how it works.
Try to rewrite your program by only using one-way if constructs and the `goto`
statement to jump in the code's flow to various labels similar to how the
assembly was structured in GDB. The source file should be named `05.goto.c`
Rewrite the code to set the boolean variable in 32-bit x86 inline assembly. Name
the source file `05.inline.c`.

## Problem #3: "Loop Constructs"

Write a program `06` to read characters from the user in a `while` loop. Count
the characters, stop on `EOF` condition, and print the total number of
characters. Take a look at the assembly in GDB. Step through the code to analyze
how it works. Try to rewrite your program by only using one-way if constructs
and the `goto` statement to jump in the code's flow to various labels similar to
how the assembly was structured in GDB for the `while` loop. The source file
should be named `06.goto.c` Rewrite the code for the `while` loop in 32-bit x86
inline assembly. Name the source file `06.inline.c`.

Write a program `07` to print all ASCII characters from code 32 up to 126 with
a `for` loop. Print the output in a tabular manner with 16 or 32 characters per
every row. Represent the constant 16 or 32 in a macro definition. Take a look at
the assembly in GDB. Step through the code to analyze how it works. Try to
rewrite your program by only using one-way if constructs and the `goto` statement
to jump in the code's flow to various labels similar to how the assembly was
structured in GDB for the `while` loop. The source file should be named
`07.goto.c` Rewrite the `for` loopin 32-bit x86 inline assembly. Name the source
file `07.inline.c`.

## GitHub Checkpoint #2, Part 1-3

For the second GitHub Checkpoint, you need to prepare, commit, and push Problem
1 through 3 to your private course repository on GitHub. You have to get the
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
2. Show how to create a directory for the first problem from the terminal.
3. Create `04.c` with all the code. Show how to compile and run it.
4. Generate assembly files for x86-64, x86, and aarch64 ISAs. Demonstrate that
   the assembly files are all different.
5. Compile assembly files to executables. Demonstrate that the machine code
   is different with `objdump` and `aarch64-linux-gnu-objdump`.
6. Try to run the three programs. Will they all run on our x86-64 server CPU?
   Try to find the answer to why it is possible to run ARM code on our server
   x86-64 CPU.
7. Create `04.inline-x86.c` with all the code. Show how to compile and run it.
8. Demonstrate that the `04.inline-x86` executable has your code in GDB.
9. Explain how inline assembly can be useful in large software projects in C.
10. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 2.

1. Connect to the server.
2. Write the program `05.c`.
3. Generate preprocessor output `05.i` for `05.c` and find out what boolean
   values are equal to.
4. Take a look at the assembly in GDB. Step through the code to analyze how it
   works.
5. Try to rewrite your program by only using one-way if constructs and
   the `goto` statement to jump in the code's flow to various labels similar
   to how the assembly was structured in GDB. Name the source file `05.goto.c`.
   Compile and test the program.
6. Rewrite part of the code in 32-bit x86 inline assembly as it was done
   during the claass. Name the source file `05.inline.c`. Compile and test the
   program.
7. Disconnect from the server.

Here is the list of things that you MUST present in the video for Problem 3.

1. Connect to the server.
2. Write the programs `06.c` and `07.c`. You will have to redirect `06.c` into
   the program `06` and redirect its output to `count.txt` file to run the first
   program.
3. Take a look at the assembly in GDB. Step through the code of both programs
   to analyze how it works.
4. Try to rewrite your programs by only using one-way if constructs and
   the `goto` statement to jump in the code's flow to various labels similar
   to how the assembly was structured in GDB. Name the source files `06.goto.c`
   and `07.goto.c`. Compile and test your program.
5. Rewrite part of the code in 32-bit x86 inline assembly as it was done
   during the claass. Name the source files `06.inline.c` and `07.inline.c`.
   Compile and run your program.
6. Disconnect from the server.

Here is the directory structure with the names of the files that you must use.

```
<Your private GitHub repository>
├── ...
├── lab-02
│   ├── problem-01
│   │   ├── 04.aarch64.s
│   │   ├── 04.c
│   │   ├── 04.inline-x86.c
│   │   ├── 04.x86-64.s
│   │   ├── 04.x86.s
│   │   └── rec.txt
│   ├── problem-02
│   │   ├── 05.c
│   │   ├── 05.goto.c
│   │   ├── 05.i
│   │   ├── 05.inline.c
│   │   └── rec.txt
│   └── problem-03
│       ├── 06.c
│       ├── 06.goto.c
│       ├── 06.inline.c
│       ├── 07.c
│       ├── 07.goto.c
│       ├── 07.inline.c
│       ├── count.txt
│       └── rec.txt
└── Readme.md
```

Here you can find the commands that will be used to compile your code.

| Problem             | Compilation Commands                                                         |
| :------------------ | :--------------------------------------------------------------------------- |
| p01: 04.c...        | `gcc -o 04 04.c` and `gcc -m32 -masm=intel -o 04.inline-x86 04.inline-x86.c` |
| p02: 05.c...        | Refer to class video                                                         |
| p03: 06.c, 07.c...  | Refer to class video                                                         |

Files `04.aarch64.s`, `04.x86-64.s`, `04.x86.s`, `05.i` may be graded manually.
Ensure that you have them in the repository. `*.s` files must include assembly
generated for different Instruction Set Architectures (x86-64, x86, aarch64).
`.i` file must contain preprocessor output.

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

#### Tools

* [GAS Syntax](https://en.wikibooks.org/wiki/X86_Assembly/GAS_Syntax)
* [GDB Quick Reference](https://users.ece.utexas.edu/~adnan/gdb-refcard.pdf)
* [Pro Git](https://git-scm.com/book/en/v2)

### Books

#### C

* C Programming: A Modern Approach, 2nd Edition by K. N. King
