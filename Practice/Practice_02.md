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

## Problem #1: "Inline Assembly"

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
`04.aarch64`. With `objdump` and `aarch64-linux-gnu-gcc` programs, observe if
the machine code for the `main` function is the same. Try to run the programs.
Try to answer why it is possible or impossible to do that.

Create a `04.inline-x86.c` file. Copy all the code from the `04.c` program.
Use the [inline GCC](https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html) x86
assembly to do the conversion from uppercase to lowercase directly in a C file.
In your assembly, you should put the input value to the `al` register, add a
certain number to switch it to uppercase according to the [ASCII table](https://en.wikipedia.org/wiki/ASCII#Printable_characters),
write the value back to the original place used by the compiler. You should
connect the C and assembly world by specifying input constraints and outlining
corrupted (clobbered) registers (in our case, just `eax`). Compile, run, and step
through your assembly instructions one by one in `gdb`. Use additional
`-m32 -masm=intel` to compile your program.

## Problem #2

TBD

## Problem #3

TBD

## GitHub Checkpoint #2, Part 1

For the second GitHub Checkpoint, you need to prepare, commit, and push Problem
1 to your private course repository on GitHub. You have to get the repository
from the instructor if you don't have one. Submit the last commit ID without any
extra characters to Canvas, pointing to the snapshot where all the code is ready.
You may create new commits and resubmit before the deadline multiple times.

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
TBD

Here is the directory structure with the names of the files that you must use.

```
<Your private GitHub repository>
├── lab-02
...
```

Here you can find the commands that will be used to compile your code.

| Problem       | Compilation Command                                   |
| :------------ | :---------------------------------------------------- |
| p01: 01.c...  | TBD                                                   |

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
