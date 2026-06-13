![[Pasted image 20250107110258.png|300]]

**Kernel:** It refers to actual program that interfaces with the hardware. So it's the core of OS.
**Shell:** It refers to the user interface for you as a human to interact with the kernel and in turn with the hardware of your computer.
- There are two variants to the shell
	- `GUI Shell:` Ex-> Mac Finder , File Explorer where you use GUI to access files.
	- `CLI Shell:` It is the alternative way to interface with the kernel.

Shell that we are going to be using is BASH Shell (Bourne Again SHell). It is a Command Line Interpreter (CLI) for the Unix system. You will find Unix based system and Unix-like system (ex LINUX, Mac OS 10) all  over the place which is completely different family from Windows and DOS.

# Why we use Command Line?
- It provides greater Control.
- Using it you can exert more control and even see hidden files and configuration files which is hidden in GUI.
- You have full Control and lot of flexibility.

>[Hacker](https://hackertyper.com/) It is actually part of LINUX kernel and written in C programming language.


# Commands

> [Resources](https://www.learnenough.com/command-line-tutorial)

```d
ls //list files and directories
cd // change directory
cd ~ //go to user root directory
cd .. //go back one level
touch // to create files
code // to open file in vs code
rm // to remove file
pwd //present working directory
rm * // to remove all files
rm -r // to remove a directory
```

>NOTE
>- Hold Alt to move the cursor to any point in Command Line in VS Code.
>- Ctrl + U => to clean current line

> **WARNING**
> To wipe your hard disk  `sudo rm -rf --no-preserve-root/`

The command line, often referred to as the **terminal**, is a text-based interface used to interact with a computer. It's an essential skill for programmers, system administrators, and power users. The shell, like **Bash (Bourne Again Shell)**, is the command-line interpreter that processes commands.

### Introduction to the Terminal and Shell

1. **Terminal**: The terminal is the environment where you type commands. In Ubuntu, the default terminal emulator is "gnome-terminal."
2. **Shell**: The shell is the program running inside the terminal. It interprets your commands and executes them. The default shell in Ubuntu is Bash.

# Anatomy of a command line

![[Pasted image 20250107135857.png|300]]

#prompt
- Every command line starts with some symbol or symbols designed to “prompt” you to action.
- The prompt usually ends with a dollar sign `$` or a percent sign `%`, and is preceded by information that depends on the details of your system.

# Commands

>_Note_: When `Ctrl-C` fails, 90% of the time hitting `ESC` (escape) will do the trick.

#man
- To get details of any command use:  `man <command-name>`
- You can even use it on man itself.
- Using arrow keys you can navigate up and down in the manual.
- Using space you can move to next page
- Press `q` to quit the manual.
![[Pasted image 20250107140737.png|400]]


![[Pasted image 20250107145718.png]]
This prints out the `$SHELL` [environment variable](https://www.cyberciti.biz/faq/set-environment-variable-unix/). If you see the result shown above, indicating that you’re already using Bash

The other possible result of `echo` is this:

```
  $ echo $SHELL
  /bin/zsh
```

If that’s the result you get, you should use the `chsh` (“change shell”) command as follows:

```
  $ chsh -s /bin/bash
```

>[meme](https://www.reddit.com/r/ProgrammerHumor/comments/vux7fd/feature/)
>[Jargon File](http://www.catb.org/jargon/html/introduction.html)
![[Pasted image 20250107142919.png|300]]

![[Pasted image 20250107143642.png|400]]

```d
About flags used in ls
-r  //to reverse the list
-l // to see data in long form
-t // to see data based on modifaction time ,Order is from older files to newer file
```
##### Hidden Files
Finally, Unix has the concept of “hidden files (and directories)”, which don’t show up by default when listing files. Hidden files and directories are identified by starting with a dot `.`, and are commonly used for things like storing user preferences. For example, in [_Learn Enough Git to Be Dangerous_](https://www.learnenough.com/git), we’ll create a file called `.gitignore` that tells a particular program (Git) to ignore files matching certain patterns. As a concrete example, to ignore all files ending in “.txt”, we could do this:

```wsl
$ echo "*.txt" > .gitignore
$ cat .gitignore
```

####  Tab completion

Most modern command-line programs (shells) support _tab completion_, which involves automatically completing a word if there’s only one valid match on the system.

```d
 $ rm tes⇥ // press (tab key) to complete the filename
```