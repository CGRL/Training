# Glossary of common Bash symbols and commands

## Syntactical Symbols

__$__ - Has two separate meanings/uses. Primarily, a `$` at the start of a variable name or construction is used to access the value stored in that variable or produced from the construction. For example, `PATH` is the name of a variable, while `$PATH` is substituted with the value of the variable. Second, `$` is often used to mark the end of your command prompt, where you can type input after the `$`.

__.__ - Has two separate meanings/uses. In file paths, `.`. indicates the current directory. At the start of a file path it denotes "relative from where I am now", and in the middle of a path is mostly useless. `.` also shows up as the the first item when you `ls -a`, indicating the directory itself. Second, a `.` at the start of a file name makes the file hidden, so it will only show up when you `ls -a`.

__..__ - In a file path, indicates the directory above or "up one level". Sometimes chained to go up multiple levels, as in `../../../somedirectory/somefile`.

__/__ - Used to separate directories in a file path. At the start of a path, indicates the root of the file tree. For example `cd /` brings you to the root, or upper-most, directory on the system.

__~__ - Called a "tilde", it indicates your `HOME` directory in a file path. Always used at the start of a path, meaning "starting from my `HOME` directory."

__\*__ - Expands to 0 or more of any characters in a file path through globbing. For example, `ls ~/*/*.txt` will list all files ending with ".txt" one level below your `HOME` directory.

__?__ - Expands to exactly 1 of any character in a file path through globbing. For example, `cat mouseRNA_R?.fastq.gz` is identical to `cat mouseRNA_R1.fastq.gz mouseRNA_R2.fastq` if those two files exist in your current working directory.

__>__ - Redirects the output of a command into a new file, named after the `>`. If a file already exists with that name, this will "clobber", or overwrite, the file.

__>>__ - Redirects the output of a command and appends it to the end of a file, named after the `>>`. Will create a new file if necessary, or append the output if one already exists.

__1>__ or __1>>__ - Redirects (or appends) only the STDOUT (regular output without errors) of a command.

__2>__ or __2>>__ - Redirects (or appends) only the STDERR (error messages) of a command.

__<__ - Directs the contents of a file into the STDIN (input stream) of a command.

__|__ - Called a "pipe", sends the STDOUT of the command  into the STDIN of the command after the `|`. Typically much faster than writing intermediate files with redirection (`>`) between commands/applications, and doesn't produce wasteful files.

__'__ - Single quotes preserve the literal value of the text between the quotes. Useful when you want to prevent substitutions and interpretation of other characters. For example, `echo '$PATH'` will output "$PATH", not the value of your `PATH` variable. Because it blocks all interpretation, you cannot nest single quotes.

__"__ - Double quotes preserve the literal value of most characters beween the quotes, but `$`, \`, and `\` will still work. For example, `echo "~"` will output "~", while `echo "$(echo ~)"` will output the path to your home directory.

__$()__ - The output of the command within the parentheses is substituted into the parent command, called command substitution. For example, `mkdir $(seq 1 5)` will make directories named "1", "2", "3", "4", and "5". Equivalent to `${}`, except that `$()` uses a subshell, so if the command alters your environment, such as by assigning a variable, those changes will not be preserved.

__\`__ - Called the "backtick", these are also used for command substitution (of the command between two backticks). They are equivalent to `$()`, except that the parenthesis are easier to nest. Triple (\`\`\`) and quintuple (\`\`\`\`\`) backticks are necessary for nesting 2nd and 3rd levels.

__${}__ - Also used for command substitution. Equivalent to `$()`, except that if the command alters your environment, such as by assigning a variable, will be preserved.

__&__ - Used at the end of a command to run it in the background, allowing you to run subsequent commands in the same terminal without having to wait until it's finished.

__&&__ - Used to separate two commands if you only want the second command to run if the first finished successfully. For example, `module load python && python` would first load Python into your environment, then, if successful, run it.

__;__ - Separates commands, equivalent to pressing ENTER. Can be used to run a sequence of commands in a single line.

## Environment Variables

__PATH__ - A list of directory paths, separated by colons (`:`), that are checked in order for executables. For example, core programs like `ls`, `mkdir`, and `ps` are usually stored in /user/bin, and this path is almost always present in your `PATH`. Installing software on Unix systems usually involves moving (or linking) the executable to a directory in your `PATH`, or adding its directory to your `PATH`.

__HOME__ - The path to your home directory.

__USER__ - Your username.

__PS2__ - Your command prompt. The value of `PS2` is printed every time the shell prompts you for your next command, and often ends with `$`.

__CWD__ - Current Working Directory. Metaphorically where you "are" in the file system, this is the current default directory for identifying which file or folder you are refering to, or where to place new files and folders.

__$1 $2 ...__ - In a Bash script, these variables reference the 1st, 2nd, and so forth, arguments supplied when running the script.

__$\*__ and __$@__ - In a Bash script, these both reference the list of all arguments supplied when running the script.

__$?__ - Stores the exit status code of the last command run. 0 indicates success, and all other numbers indicate failure.

## Commands

__cd__ - Change Directory. Used to change your current working directory.

__pwd__ - Print Working Directory. Essentially, "Where am I?"

__mv__ - MoVe. Moves a file or directory to a new directory, and/or renames the file.

__cp__ - CoPy. Copies a file (1st argument) into a new file named by the 2nd argument.

__rm__ - ReMove. Permanently deletes a file or directory.

__ls__ - LiSt. Lists all directories and files in the designated directory (default `CWD`).

__mkdir__ - MaKe DIRectory. Creates a directory with the given name.

__ln__ - LiNk. Without creating a second copy, creates a link (or "shortcut") to a file or folder in another directory.

__touch__ - Updates the timestamp of a file. If the file does not exist, touch will create an empty file.

__cat__ - conCATenate. Dumps the entire contents of one or more files to your normal output (STDOUT), in order.

__less__ - A simple file viewer that allows you to scroll up and down. `less` is a play on words, from the phrase 'less is more', because an older file viewer was named "more", after the "MORE" prompt at the bottowm that allowed it to scroll down (but not up).

__grep__ - Gnu Regular Expression Print. Searches one or more files for a query string. The "regular expression" part allows it to search for complex patterns, as well as specific strings.

__echo__ - Simply prints the value of a variable or expression. Useful for checking values, or for piping specific short input into other programs.

__tee__ - Forks an input stream (STDIN) into a file as well as STDOUT. Used when you want to redirect and pipe your output at the same time.

__which__ - Prints the full path to an executable found in your PATH. Useful for finding where software is installed, and for discovering *which* version of a particular software you are running by default when multiple versions are installed.

__source__ - Runs a shell script in the current shell environment. By default, shell scripts are run in subshells, so any variables or other environmental changes won't persist outside of the context of the script. `source`ing a file lets you use variables set within the file in your current session.

__export__ - Sets an environment variable to be inherited by child processes. Ordinarily, environment variables you set will only be available to the Bash process you are running. This changes that so that other programs you run can access the designated variable.

__alias__ - Lets you give short, custom names to long commands. An alias is like a variable, except it's value is automatically substituted when its name is interpreted by the shell.

__du__ - Disk Usage. Reports the disk usage of directories and files.

__df__ - Disk Free. Reports the total disk usage and free space for all file systems.

__chmod__ - CHange MODe. Sets file permissions, as well as personal and group ownership.

__chgrp__ - CHange GRouP. Changes group ownership for file/s and directories.

__chown__ - CHange OWNer. Changes the personal ownership for file/s and directories.

__groups__ - Lists all groups you are a member of.

__passwd__ - Changes your password.

__sudo__ - Super User DO. Runs the following command as a Super User (admin). Requires high level priveliges.

__su__ - Switch User. If another username is supplied, switches to that user. If none supplied, attempts to switch to root (master admin).

__ps__ - ProceSses. Lists currently running processes.

__top__ - A handy utility to display all processes, sorted by CPU usage (default) or other resource usage, as well as a summary of total system resource usage.

__kill__ - Terminates a process by process ID.

__sleep__ - Causes the shell to wait for the indicated number of seconds.

__nohup__ - NO HangUP. Causes the following command/application to continue running after you close your terminal or log off.

__sort__ - A handy (and efficient) tool to sort lists of data.

__cut__ - A handy tool to separate out columns from tabular data.

__sed__ - Stream EDitor. A utility that performs textual manipulations (e.g. find/replace) on a stream of input data.

__tar__ - Archives mutliple files/directories into a single file, called a "tarball". The name comes from "Tape ARchive". Can also compress and extract archives.

__gzip__ - Gnu ZIP. A common compression tool.

__find__ - Locates files and directories.

__rename__ - Uses patterns to rename many files.

__ping__ - Sends basic queries over a network, such as to an IP address or domain name and reports whether and how long it took for the target to respond. Usefull for testing network or internet functionality.

__ifconfig__ - Reports and sets the configuration of your network.

__ssh__ - Secure SHell. A program (and protocol) for establishing encrypted connections over a network. Often used to log in to remote servers.

__scp__ - Secure CoPy. Uses SSH to transfer files over a network.

__ftp__ or __ftps__ or __sftp__ - File Transfer Protocol. A program (and protocol) used to transfer files over the internet. `ftps` and `sftp` are encrypted variants.

## Files

__.bashrc__ - bash Run Commands. A file containing a list of commands that get run when you start a new shell. This file is commonly used to configure your default shell environment, such as by adding to your `PATH`, assigning other variables, or assigning aliases.

__.bash_profile__ - Almost the same as .bashrc, except .bash_profile is run when you log in to a new system. Functionally the same on remote systems, but on your Unix-based PC, including MacOS, .bash_profile gets run when you reboot, while .bashrc gets run every time to open a new terminal.

__~/.ssh/config__ - The configuration file for ssh is usually kept in a hidden directory in your home directory. It lets you set default options overall as well as for various servers, which can be very helpful when you often work on remote machines.

__~/.ssh/known_hosts__ - A file that contains the public keys (like cryptographic fingerprints) of all the ssh servers you've connected to. If you connect to a server with the same domain, but it has a different key, you will get a warning message or automatically abort the connection. This is because a bad actor may be spoofing the domain and trying to trick you into giving them your login and password.
