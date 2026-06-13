- `/` (slash) refers to the system's root directory
- hence `cat /` takes you to root dir.
- `cat dir1/d1/file1` is relative path as it starts without slash.
- `cat/home/user100/dir1/d1/file1` is an absolute path.
- `cat ../D2/myfile` is also a relative path


#### Using vim in bash

- `vi file_name` to create file
- Two modes of vim (use `ESC` to switch ):-
	- Command mode (by default) : here you can give command like `wq` to save without quit.
	- Insert mode (to type) - press `i` key after pressing `ESC`
	- Append mode

#commands

```d
`:!q` - to quit after override.

```


![[WhatsApp Image 2025-01-16 at 18.50.44_671d6f8a.jpg|400]]
**Corrections**
- `0 (zero)`  is for beginning  of file not `O`
- `$` is to go to end of line
- `Ctrl+R` is to go backward to expression
- `w file` to save file with different name


# Files and Directories  permissions

Length of permission string - 10

_ | _ _ _ | _ _ _ | _ _ _
Ex: `drwxr-xr-x`

- 1st dash tells if it is file or directory : d- directory ,, dash means file
- Now there are three groups of 3 dash each.
	- 1st group is to set the permission for Owner denoted by `u`
	- 2nd group is to set the permission for Group(g) denoted by `g`
	- 3rd group is to set the permission for Others denoted by `o`
	- To assign permission to all use `a`
- There are three permission that are set in order in each group.
	- This should be in order like `rwx` , here:
		- r is read
		- w is write
		- x is execute
- Use `chmod` command to set permission like:
	- `$ chmod u=rwx,g+rw,o-r file2.txt`
		- `=`replaces the previous permission with the assigned permission.
		- `+` appends the assigned permission
		- `-` removes the assigned permission
- By default executable permission is not provided to the file
![[Pasted image 20250120202949.png||400]]

- By default write permission of a folder is not given to group and others.

```d
we can write following flag for additional info
`-v` -> to give a statement that what permission is set to what
`-R` ->  to 
```


# Numeric way to set permission
```d
rwx -> _ _ _ -> 4 2 1 in binary
so to set:
r -> 4
wx-> 3
x-> 1
rwx -> 7
```
# umask

- It is stored in hidden file `.bashrc`
- In case of files it is calculated by `666 - provided values.`
- By default provided value for file is `022` so permission set are `644`.
- In case of folder it is calculated by `777 - provided values`.


#passwd
Uses:
- To reset the password.
- Admin can change the password of any username
- Whenever you set the password then the encrypted password is shown in `/etc/shadow` .It cannot be seen with cat.
```d
passwd -d username
//to delete password of any username
exit //use it before testing
su - username
passwd -l username // user will not be able to login
//to fix set a new password
passwd -e username // to expire the password of user and user has to set new password
```

```d
useradd
passwd
mkdir
chown
adduser
chmod
```


# add user command

This command is better than `useradd` command.
```d
adduser testuser1
```
- when a new user is created then it get's assigned an unique ID.
- It also get added to a group automatically which has the same name as the user added.This group is primary group of this user.Even id of user and group is same.
- user entry is in /etc/passwd file
- group entry is in /etc/group file
- passwords are stored in /etc/shadow file
- It also copy files from /etc/skel .The files and directories stored in this folder is automatically added to the added user account.
- The added user will also get added in secondary group `users`.
- Even the prompt of the terminal will be in format `username@LAPTOP_NAME:~#`

# echo command

- It is used to get the absolute path of the user

```d
echo ~
echo ~testuser1
echo ~root
```

# About /etc/passwd

```d
username:password:user_id:primary_group_id:command_field:user_home_directory:shell_type(bash)
//When user login's then shell file in 7th field gets executed
```



# To block the user

```d
# chsh -s/usr/sbin/nologin <username>
```
- It removes the entry from the 7th field in `/etc/passwd` file and replace with 
- If you try to login then you will get `This account is currently not available.`
- You can also change this displayed message by add files in home file from root.
	- You can make a folder in home with any name let's say `security`.
	- Write following content in it:
		- `#!/usr/bin/tail +2`
		- After this line you can write the msg to be displayed.
	- As it should be executed in another user the run following command:
		- `#chmod 755 security`
	- Now run following command
		- `#chsh -s/home/security username`
- To unblock the user
	- use `chsh -s/bin/bash username` 


# APT
- It stands for Advanced Packaging Tool
- APT commands which results in change in system should run from root or use `sudo` to run them
```d
//Installing packages
sudo apt install <package_name>
//Removing packages
sudo apt remove <package_name>
//updating package index - It only updates the package version
sudo apt update
//uprading packages - It upgrades the ubuntu system by installing all updated packages.
sudo apt update
sudo apt install
//List packages based on package names
apt list
//To get package details - It doesn't tell about the location of package
apt show <package_name>
apt show tree
apt show ncal
//To get location data
apt install apt-file // if not installed
apt update //if not installed
apt-file list <package_name>
```
- Adding `--purge` option with remove will also remove the package along with its configuration files as well , so use it with caution.
- All log files of installed package is kept under `/var/log/dpkg.log` file.
- APT is newer than the dpkg and dpkg commands can also run on ubuntu
	- List Packages : `dpkg -l`
	- List Package installed files:  `dpkg -L <package_name>`
	- Installing package: `dpkg -i <package_name>` 
		- It requires `.deb` files.
	- Removing package: `dpkg -r <package_name>`


# grep command
- Also called filter command.

![[Pasted image 20250130191627.png]]
![[Pasted image 20250130191638.png]]
![[Pasted image 20250130191920.png]]



# Shell Scripting

- you can create `.sh` file for creating execution file.
To run this file there are 2 ways:
1. `sh myscript.sh`
2. `./myscript.sh`
	- but before running this command you need to provide execution permission
	- `chmod 744 myscript.sh`



# egrep command
The key differences between `egrep` and `grep` are:

| Feature                                 | `grep`                                                                    | `egrep`                                                                               |
| --------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Extended Regular Expressions (EREs)** | Uses **Basic Regular Expressions (BREs)**                                 | Uses **Extended Regular Expressions (EREs)**, allowing more powerful pattern matching |
| **Metacharacter Handling**              | Metacharacters like `+`, `?`, `{}` need to be escaped (`\+`, `\?`, `\{}`) | Metacharacters are used directly without escaping                                     |
| **Performance**                         | Slightly slower for complex patterns                                      | Optimized for handling complex expressions, making it faster in some cases            |
| **Usage Command**                       | `grep "pattern" file`                                                     | `egrep "pattern" file` (or `grep -E "pattern" file` in modern versions)               |
| **Status in Modern Systems**            | Still widely used                                                         | Deprecated in some systems, replaced by `grep -E`                                     |
|                                         |                                                                           |                                                                                       |
![[Pasted image 20250210201102.png]]

![[Pasted image 20250210202821.png]]

![[Pasted image 20250210203702.png]]

