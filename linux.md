# Linux & Shell Notes

## Terminal

**Terminal** - It's a program that accepts text based commands and can render text on the screen.

## Shell

**Shell** - Shell do a lot of things, but their main job is to interpret the commands you type and execute them.

Shell is often referred to as a **REPL**:
- **R**ead
- **E**val
- **P**rint
- **L**oop

```bash
expr 1111 + 1111
```
**expr** - A command that evaluates and prints the result of a mathematical expression.

### Local Variables

```bash
name="Zoro"
anime="One Piece"
echo "$name is from $anime"
```

---

## File Systems

```bash
pwd
```
**pwd** [print working directory] - Prints the path of the directory you're currently in.

```bash
ls
```
**ls** - Displays the contents (files and folders) of the current directory.

```bash
ls worldbanc/
```
Display the contents of `worldbanc` without moving into it.

```bash
cd ~
```
**cd ~** - Takes you to the root/home directory.

```bash
cd ..
```
**cd ..** - Moves you out one level up from the current directory.

### Absolute and Relative Paths

- **Absolute paths** start at the root of the filesystem `/`
  - ex. `/vehicles/cars/fords/mustang.txt`
- **Relative paths** take the current directory into account
  - ex. When inside the top-level `vehicles` directory, the relative path to the mustang.txt file is:
  `cars/fords/mustang.txt`

### cat [catenate]

```bash
cat tbills.txt
```
Command to read the contents of a file, display contents of multiple files.

### head and tail

To read the first and last n lines of a file:
```bash
head -n 6 2023.csv
tail -n 6 2023.csv
```

### more and less

To enter interactive mode:
```bash
less 2023.csv
```
To enter interactive mode with line numbering:
```bash
less -N 2023.csv
```

### touch

- Updates the access and modification timestamps of a file.
- If the specified file does not exist, this command creates a new empty file.

---

## Directories

### mkdir [make directory]

Creates a new directory inside the current directory.

### move

Moves a directory or file from one location to another location.
```bash
mv credit_cards/tbills.txt investments/tbills.txt
```

### remove

Deletes a file or empty directory.
```bash
rm tbills.txt
```
Use the `-r` flag to delete a directory and all of its contents recursively.
```bash
rm -r directory_name
```

### copy

It copies a file from one location to another.
```bash
cp source_file.txt destination/
```
To copy a directory and all of its contents recursively, add a `-R` flag.
```bash
cp -R my_dir new_dir
```

### ~ Alias

```bash
cd ~
```
Takes you to home.

### grep

Allows you to search for text in a file.
```bash
grep "CRITICAL" file_name.txt
grep "CRITICAL" file1.txt file2.txt
```
Use the `-r` flag for recursive search in the current directory and all subdirectories.
```bash
grep -r "CRITICAL" .
```
`.` is a special alias for the current directory.

### find

To find a file by name:
```bash
find some_dir -name hello.txt
```
Pattern searching:
```bash
find some_dir -name "*.txt"
find some_dir -name "*dad*"
```

---

## Permissions

```bash
whoami
```
**whoami** - Prints the username of the currently logged-in user.

```bash
sudo whoami
```
**sudo** - Runs a command with superuser (admin) privileges.

Permissions control who can do what to which files and directories. The permission of an individual file or directory is visually represented as a 10-character string.

- Directory: `drwxrwxrwx`
- Regular file: `-rwxrwxrwx`

`r`-read, `w`-write, `x`-execute
- `rwx` - all permissions
- `rw-` - read & write, but not execute
- `r-x` - read & execute, but not write

The first three characters are **owner** permissions, the next three characters are **group** permissions, and the last three are for **others** permissions.

```bash
ls -l my_dir
```
To view who has what permissions.

### Change Permissions

**chmod command** [change mode] - Changes permissions.
```bash
chmod -R u=rwx,g=,o= dir_name
chmod -x genids.sh   # remove the executing permission of the file
chmod +x genids.sh   # add executing permission
```

```bash
rm -rf
```
Can delete every file in the system. `-r` recursive, `-f` forcefully.

### chown command [change owner]

Changes the owner.
```bash
sudo chown -R root my_dir
```

---

## Programs

```bash
./filename.sh
```
To execute a file.

### Shebang

Is a special line at the top of a script that tells your shell which program to use to execute a file.
```bash
#! interpreter [optional-arg]
#!/usr/bin/env bash
```

```bash
ls -a ~
```
**ls -a** - Lists all contents of a directory, including hidden files.

```bash
nano ~/.bashrc
```
**nano** - A simple, beginner-friendly command-line text editor used to open and edit files.

`sh`, `bash`, `zsh` - [shell, bourne again shell, z-shell]

---

## Environment Variables

```bash
export NAME="zoro"    # always use capital letters
$NAME
```

### PATH

**PATH** - An environment variable that lists the directories the shell searches through to find executable programs.

Add to the path:
```bash
export PATH="$PATH:/absolute_path"
```

---

## Man Pages & Flags

```bash
man command-manual
man man
man cat
```
**man** [manual] - Opens the manual page for a command, showing how to use it.

**Flags** - Optional switches added to a command (usually starting with `-`) that change its behavior.
```bash
ls -l   # long list
ls -a   # list with hidden files
ls -la
```

### Positional Arguments

```bash
mv credit_cards/tbills.txt investments/tbills.txt
```
`mv` command took two positional arguments.

### Exit Codes

To access the status of the last ran program:
```bash
echo $?
```

---

## Input / Output

### Standard Output

```bash
echo "hello world"
```

### Standard Error

`>` redirects stdout, `2>` redirects stderr.

```bash
echo "hello world" > hello.txt
cat hello.txt
```

```bash
echo doesnotexist.txt 2> error.txt
cat error.txt
```

### Standard In

```bash
read NAME
echo $NAME
```

### Piping

**Piping** (`|`) - Takes the output of one command and feeds it as input into another command, letting you chain commands together.

```bash
grep -R "Bob" 2020.csv 2021.csv 2022.csv 2023.csv --exclude-dir="backups" | wc -l
```

---

## Process Management

### Interrupt

To stop a program using `ctrl+c`.

### kill

```bash
ps aux
```
`ps aux` - To display a complete snapshot of all currently running processes on the system.
```bash
ps aux | grep "filename.txt"
kill process_id[PID]
```

### top

Allows you to see which programs are using the most resources on your computer.
```bash
top
```

---

## Packages

```bash
nvim
```
**nvim** - A terminal-based text editor (Neovim), used to open and edit files.

```bash
lsd --tree
```
**lsd** - A modern replacement for `ls` with icons and colors. The `--tree` flag displays files and directories in a tree structure.

## Download

```bash
wget https://github.com/bootdotdev/worldbanc/archive/refs/heads/main.zip && unzip main.zip && rm main.zip && mv worldbanc-main world-bank
```
**wget** - Downloads a file from a URL onto your machine.
**unzip** - Extracts the contents of a `.zip` file.

This command chains four steps together with `&&` (run the next command only if the previous one succeeds):
1. `wget ...` downloads the zip file from GitHub
2. `unzip main.zip` extracts it into a folder
3. `rm main.zip` deletes the now-unneeded zip file
4. `mv worldbanc-main world-bank` renames the extracted folder to `world-bank`
