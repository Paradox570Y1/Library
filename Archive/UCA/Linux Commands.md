# VIM

- To select multiple lines use `v` or `Shift+v` after pressing `Esc`.
	- Then use arrow keys or `j/k` to select lines up and down.
- To copy text from wsl ubuntu to window machine use
	![[Pasted image 20250805203629.png|300]]
- To copy whole code
	- Use `%w !clip.exe`
- You can run programs directly while in vim mode
	- Use something like `:!javac file.java` and `:!java file`

#### To execute c codes in Linux
- check if gcc is installed `gcc --version
- To install run `sudo apt install gcc`
- To compile code `gcc program.c -o program`
- To run it `./program`

> To copy text and paste downward - `yyp`
> To copy text and paste upward - `yyP` 
> To delete current line - `dd`
> Do above in normal mode by pressing `Esc`


#### To replace text on vim
![[Pasted image 20250805212849.png|200]]

# To undo Pasting in VIM
### 1️⃣ If you just pasted and haven’t done anything else

- Press `u` (in **normal mode**) → undoes the last change (the whole paste is one change).
- Press `Ctrl + r` to redo if you undo too far.


![[Pasted image 20250815214654.png]]
# Formatting code

- use `=` to format 
- use `gg=G` to format whole code


# To install debugger
`sudo apt-get install gdb`

![[Pasted image 20250815215034.png]]

`b main`- adds breakpoint at main
`b merge` - adds breakpoint at merge
`c` - continue
`r` - run
`q` - quit


