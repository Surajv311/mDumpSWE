
# Linux_internals_and_commands


- `sudo`: Sudo is a command in Linux allows users to run commands with privileges that only root user have.
- `grep -i "UNix" geekfile.txt`: Case insensitive search
- `grep -c "unix" geekfile.txt`: Displaying the count of number of matches
- `grep -l "unix" *` (or) `grep -l "unix" f1.txt f2.txt f3.xt f4.txt`: Display the file names that matches the pattern
- `grep -w "unix" geekfile.txt`: Checking for the whole words in a file
- `head <file>` Displays the first parts of files, with the syntax, head [options] [file_name].
- `tail <file>`: Displays the last N number of lines of the given input.
  - `tail -f /var/log/syslog`: It only shows the last part of the logs, where problems usually lie. tail will continue watching the log file and print out the next line written to the file.
  - If you do: `pip install -r /tmp/requirements.txt --ignore-installed | tee /tmp/pip_installation.log` - It will install pip requirements packages as well as output the process in `pip_installation.log` file. You can watch this log file using tail command: `tail -f pip_installation.log`
- `cat <file_name>`: View file content
  - Eg: `cat <file> | head -88 | tail -1`: To display the 88th line of a file 
- `fdisk -l`: The fdisk command is used for disk partitioning and disk management on Unix-like systems. The -l option lists information about all available disks and their partitions. This command is typically used to view the current disk layout and partitioning scheme of the system.
- `ps -ef`: The ps command is used to display information about running processes on Unix-like systems. The -ef options stand for "everyone" (-e) and "full-format" (-f), which together instruct ps to display information about all processes in a detailed format. This includes information such as the process ID (PID), the terminal associated with the process, the user running the process, CPU and memory usage, and the command being executed.
  - `ps -ef | grep pip`: Lists down all running processes by the name pip. 
- `ls -l <dir path else it lists current path files>`: Lists files and directories in the specified directory (or the current directory if none is specified) with detailed information, including permissions, ownership, size, and modification date.
- `ls -lrt`: Lists files and directories in the current directory in long format (-l) sorted by modification time in reverse order (-r for reverse, -t for time).
- `pwd`: Prints the current working directory.
- `ls -la`: Lists all files (including hidden files) and directories in the current directory in long format, showing detailed information, including hidden files (-a for all).
- `su`: Allows switching to another user account. If no username is specified, it defaults to the superuser (root) account.
- `su root`: Switches to the root user account.
- `whoami`: Displays the username of the current user.
- `who`: Lists about users who are currently logged in to the system.
- `last`: This command in Linux is used to display the history of last logged in users.
- `which python`: Displays path where executable file of python is located.
- `top`: Displays real-time information about system processes, including CPU and memory usage.
  - In your keyboard if you press button 'c' after running top command - it will display the stats in detailed manner. There are other keyboard buttons as well to press which would display other functionalities with top command. 
- `set | grep AWS_KEY`: Displays environment variables (set) and filters the output to show lines containing AWS_KEY using grep.
- `screen -S vikas`: Starts a new screen session with the name vikas.
  - `screen -ls`: Lists currently running screen sessions. screen command in Linux provides the ability to launch and use multiple shell sessions from a single ssh session.
- `find ~ -name aws_credentials`: Searches for files named aws_credentials in the user's home directory (~).
  - `find / -name "requirements.txt" 2>/dev/null`: Searches for file from root directory. The /dev/null command suppresses error messages about directories you don't have permission to read.
  - `find . -name "requirements.txt"`: Command will search for the file starting from the current directory (.) and look through all subdirectories.
  - `find / -type d -name "efs"`: Command will search for a directory with name "efs".
- `grep -iR AWS_KEY *`: Searches recursively (-R) for occurrences of AWS_KEY in files in the current directory and its subdirectories (*).
- `exit`: Exits the current shell or session.
- `grep -iR access <path>`: Searches recursively for occurrences of access in files within the specified path.
- `echo $ec2`: Prints the value of the environment variable ec2.
- `pip install -U s3fs=0.4.0`: Installs or upgrades the s3fs Python package to version 0.4.0 using pip.
- `cd ./venvs`: Changes the current directory to venvs, which is located in the current directory (.).
- `df -h`: The df command is used to display disk space usage on Unix-like systems. The -h option stands for "human-readable" and formats the output in a more easily understandable way, showing sizes in kilobytes, megabytes, gigabytes, etc., rather than in raw bytes.
- `du psycopg2-2.9.3.tar.gz`: Displays the disk usage of the psycopg2-2.9.3.tar.gz file.
- `du -sh psycopg2-2.9.3.tar.gz`: Displays the disk usage of the psycopg2-2.9.3.tar.gz file in a human-readable format (-h) and summarizes the total (-s).
- `du -sh *`: Displays the disk usage of all files and directories in the current directory in a human-readable format and summarizes the total.
  - `sudo du -sh /*`: Displays disk usage for all files/directories with root user privilege. 
- `du -sh * | sort -h`: Displays the disk usage of all files and directories in the current directory in a human-readable format, summarizes the total, and sorts the output numerically and in a human-readable way (-h).
- `conda list`: Lists installed packages and their versions using Conda, a package manager for Python.
- `echo $PATH`: It prints out the value of the PATH environment variable. 
- `sudo -su user`: It is short for sudo -s -u user. The -s option means to run the shell specified in the environment variable SHELL if this has been set, or else the user's login shell. The -u user option means to run the command as the specified user rather than root. 
- `sudo su user`: It will use sudo to run the command su user as the root user. The su command will then invoke the login shell of the specified username. The su user command could be run without the use of sudo, but by running it as root it will not require the password of the target user.
- `rm /path/to/directory/*`: To remove all non-hidden files* in a directory 
- `rm -r /path/to/directory/*`: To remove all non-hidden files and sub-directories (along with all of their contents) in a directory
- `rm -rf "/path/to the/directory/"*`: Force removal of files
- `history`: Provides a chronological list of previously executed commands
- `bash`: bash is a command interpreter, a shell, a program with an interface that interprets the commands that you put into it.
- `pstree`: To know how many sub-shells deep you are. 
- `netstat`: The network statistics command is a networking tool used for troubleshooting and configuration, that can also serve as a monitoring tool for connections over the network.
- `ps aux`: Similar to `ps -ef`. Displays information about running processes. 
- `ssh -i`: To ssh into a machine. '-i' is identity_file which selects a file from which the identity (private key) for public key authentication is read. 
- `ping -c 1 $(hostname)`: To get IP address of the machine
- `watch`: Used to execute a program periodically, showing output in fullscreen.
  - `watch -n 1 "ps -ef | grep ssh"`: Executes `ps -ef | grep ssh` command every second and displays output. 
- `kill -9 <pid>`: To kill a process/pid. 
  - In Linux, an executable stored on disk is called a program, and a program loaded into memory and running is called a process. When a process is started, it is given a unique number called process ID (PID) that identifies that process to the system. If you ever need to kill a process, for example, you can refer to it by its PID.
  - In addition to a unique process ID, each process is assigned a parent process ID (PPID) that tells which process started it. The PPID is the PID of the process’s parent.
  - Eg case: 
  ```
  ubuntu@ip-10-80-10-5:/tmp$ ps -ef | grep 17600
  root       17600   17599  0 Jul04 pts/2    00:00:00 ssh ubuntu@10.80.10.5 pip install -r /tmp/requirements.txt --ignore-installed
  ubuntu     47424   42931  0 09:41 pts/3    00:00:00 grep --color=auto 17600
  ubuntu@ip-10-80-10-5:/tmp$ ps -ef | grep 17599
  root       17599   17598  0 Jul04 pts/2    00:00:06 /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1720107928.4152038-772178-155392337109202/AnsiballZ_command.py
  root       17600   17599  0 Jul04 pts/2    00:00:00 ssh ubuntu@10.80.10.5 pip install -r /tmp/requirements.txt --ignore-installed
  ubuntu     47422   42931  0 09:41 pts/3    00:00:00 grep --color=auto 17599
  ubuntu@ip-10-80-10-5:/tmp$ ps -ef | grep 17598
  root       17598   17597  0 Jul04 pts/2    00:00:00 /bin/sh -c echo BECOME-SUCCESS-ajehwmoeqrbnefnxsyzfglmuqbkerlqz ; /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1720107928.4152038-772178-155392337109202/AnsiballZ_command.py
  root       17599   17598  0 Jul04 pts/2    00:00:06 /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1720107928.4152038-772178-155392337109202/AnsiballZ_command.py
  ubuntu     47429   42931  0 09:41 pts/3    00:00:00 grep --color=auto 17598
  ubuntu@ip-10-80-10-5:/tmp$ ps -ef | grep 17597
  root       17597   17596  0 Jul04 pts/2    00:00:00 sudo -H -S -n -u root /bin/sh -c echo BECOME-SUCCESS-ajehwmoeqrbnefnxsyzfglmuqbkerlqz ; /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1720107928.4152038-772178-155392337109202/AnsiballZ_command.py
  root       17598   17597  0 Jul04 pts/2    00:00:00 /bin/sh -c echo BECOME-SUCCESS-ajehwmoeqrbnefnxsyzfglmuqbkerlqz ; /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1720107928.4152038-772178-155392337109202/AnsiballZ_command.py
  ubuntu     47467   42931  0 09:43 pts/3    00:00:00 grep --color=auto 17597
  ```
- `cd /proc/<your pid>/fd`: [To get process details from its PID, we use it](https://stackoverflow.com/questions/29105448/get-process-info-from-proc). Post `cd` into the directory we can run `ls` or `cat` command and get infos on processes. Eg: `sudo ls -l /proc/330046/fd/1`
  - Cases: 
  ```
  /proc/cpuinfo: Information about the processor, such as its type, make, model, and performance.
  /proc/[pid]/cmdline: This holds the complete command line for the process, unless the whole process has been swapped out, or unless the process is a zombie. In either of these later cases, there is nothing in this file: i.e. a read on this file will return 0 characters. The command line arguments appear in this file as a set of null-separated strings, with a further null byte after the last string.
  /proc/[pid]/cwd: This is a link to the current working directory of the process.
  /proc/[pid]/environ: This file contains the environment for the process. The entries are separated by null characters, and there may be a null character at the end.
  /proc/[pid]/exe: The exe file is a symbolic link containing the actual path name of the executed command. The exe symbolic link can be dereferenced normally – attempting to open exe will open the executable. You can even type /proc/[pid]/exe to run another copy of the same process as [pid].
  /proc/[pid]/fd: This is a subdirectory containing one entry for each file which the process has opened, named by its file descriptor, and which is a symbolic link to the actual file (as the exe entry does). Thus, 0 is standard input, 1 standard output, 2 standard error, etc.
  /proc/[pid]/maps: A file containing the currently mapped memory regions and their access permissions.
  /proc/[pid]/mem: The mem file provides a means to access the process memory pages, using open, fseek and read commands.
  /proc/[pid]/root: This is a link to the root directory which is seen by the process. This root directory is usually “/”, but it can be changed by the chroot command.
  /proc/[pid]/stat: This file provides status information about the process. This is used by the Process Show utility. It is defined in fs/proc/array.c source file and may differ from one distribution to another.
  /proc/devices: List of device drivers configured into the currently running kernel.
  /proc/dma: Shows which DMA channels are being used at the moment.
  etc etc...
  ``` 
- `cmp <source path file> <destination path file>`: It is used to compare the two files byte by byte and helps you to find out whether the two files are identical or not.
- `cp <source path file> <destination path file>`: Command creates a copy of the source_file at the specified destination.
- `sh test_file.sh `: To run a shell script. sh is the bourne shell. There are several shells, of which bourne is the old standard, installed on all unix systems, and generally the one you can guarantee will exist. The shell is the command interpreter that takes your input, provides output back to the screen, to the correct files, etc, and provides all the basic built-in commands you need to manage jobs, kill, test expressions, etc. Your command above is saying to run that shell-script using the bourne shell. Different shells use different syntax, so using the correct shell is a requirement. The first line of the shell should also define which to use: #!/bin/sh says use /bin/sh.
  - The -c option in the sh command is used to execute a command or a series of commands provided as an argument to the -c option. Eg: `sh -c "command1; command2; command3"`
- `chmod a+x test_file.sh`: The chmod a+x command in Linux adds the execute permission to a file for all users (owner, group, and others). All [chmod commands _al](https://www.geeksforgeeks.org/chmod-command-linux/).
  - [File permissions control _al](https://www.freecodecamp.org/news/file-permissions-in-linux-chmod-command-explained/) which actions can be performed by which users. Read, Write, and Execute are the three actions possible for every file. Three important commands you'll use when managing file permissions: chmod (Change mode), chown (Change ownership), chgrp (Change group).
  - Users are classified under three broad categories: Normal users, Groups, and Others. Linux allows users to set permissions at a very granular level. You can secure your file or directory in every possible location of a file system.
  - chmod is a command that lets you change the permissions of a file or directory to all types of users.
    - user level permissions: u – Grant permission to a user; g – Grant permission to a group (A Group of users); o – Grant permission to others 
    - file level permissions: r – Grants read permission; w – Grant write permission; x – Grant execute permission
  - We can execute .sh files by just running them like this, eg: `./install.sh`. But it is possible file may not execute, for such case, we need to change the relevant permissions, eg: `chmod +x install.sh` and then run. To remove permissions, one could run `chmod -x install.sh`.  Similarly, say to remove read permissions: `chmod -r install.sh`.
- `sudo dmesg`: All the messages received from the kernel ring buffer is displayed when we execute the command “dmesg”, here only the latest messages will be shown.
  - The kernel ring buffer can be thought of as a log file, but for the kernel itself. However, unlike other log files, it's stored in memory rather than in a disk file.
- `sudo apt-get install iftop`: apt-get (Advanced Packaging Tool) is a command-line tool that helps in handling packages in Linux.
  - Similarly to uninstall: 
    - `apt-get remove iftop`: will remove the binaries, but not the configuration or data files of the package packagename. It will also leave dependencies installed with it on installation time untouched.
    - `apt-get purge iftop`: will remove about everything regarding the package packagename, but not the dependencies installed with it on installation. Both commands are equivalent. Particularly useful when you want to 'start all over' with an application because you messed up the configuration. However, it does not remove configuration or data files residing in users home directories, usually in hidden folders there. There is no easy way to get those removed as well.
    - `apt-get autoremove`: removes orphaned packages, i.e. installed packages that used to be installed as an dependency, but aren't any longer. Use this after removing a package which had installed dependencies you're no longer interested in.
    - `aptitude remove iftop`: will also attempt to remove other packages which were required by packagename on but are not required by any remaining packages. Note that aptitude only remembers dependency information for packages that it has installed.
    - [etc, etc... _al](https://askubuntu.com/questions/187888/what-is-the-correct-way-to-completely-remove-an-application) 
- `clear`: Clear the terminal screen in Linux
- `date`: Displays date in UTC in linux
- `scp <file/host> <file/host>`: scp (secure copy) command in Linux system is used to copy file(s) between servers in a secure way. The SCP command or secure copy allows the secure transferring of files between the local host and the remote host or between two remote hosts. It uses the same authentication and security as it is used in the Secure Shell (SSH) protocol. SCP is known for its simplicity, security, and pre-installed availability.
  - Eg: `sp -r circleci@13.120.15.80:/home/repo/file/values.yml migrated_values.vml`
  - `scp user@remotehost:/home/user/file_name`: Securely copy a file from remote machine to our local machine
  - `scp [file_name] remoteuser@remotehost:/remote/directory`: Securely copy a file from a local machine to a remote machine
- `cat /etc/passwd`: To list all users in a Linux system you can read the file (as seen). Each line in this file represents a user account, and the first field in each line is the username.
- `cat /etc/group`: The /etc/group file is a configuration file on Unix-like systems that stores the group information for the system. It contains a list of groups, each with a unique group name and a list of users who are members of that group.
- `cat /etc/sudoers`: The /etc/sudoers file is a configuration file on Unix-like systems that specifies which users or groups are allowed to run commands with superuser (root) privileges using the sudo command.
- `tcpdump`: It is used to capture, filter, and analyze network traffic such as TCP/IP packets going through your system.
- In terminal, if you type a long command, and want to move the cursor to first alphabet/position, press: `Ctrl + a` in keyboard. 
- In terminal, if you want to retrace and use a command previously/historically used, click `Ctrl + r` in keyboard and search the command in terminal, for further historical instance, click `Ctrl + r` again and again. 
- `cat date_2024_08_04_data.csv | wc -l`: 'wc' stands for word count. In given command we count the no. of lines in the file. 
- Run gunzip zip/unzip command(s) and tar file commands: 
  - `gunzip originalGeoIP2-City.tar.gz` (unzip file) -> `tar -xvf originalGeoIP2-City.tar` (decompress tar file) -> `tar -cvf gunzipTarGeoIP2-City.tar GeoIP2-City_20230512/` (compress folder to tar file) -> `gzip gunzipTarGeoIP2-City.tar` (zip back)
- `md5sum file.yml`: The MD5 sum of a file is a 32-character hexadecimal number that verifies a file's integrity. It's commonly used to check if a file has changed due to a disk error, faulty transfer, or other reasons.
- `aws cloudwatch describe-alarms --query "MetricAlarms[].[AlarmName, AlarmActions]" | jq -r '.[] | select(.[1] != null) | "\(.[])"'`: The command you provided is a combination of AWS CLI and the jq tool, which is used for processing JSON data. The entire command retrieves a list of CloudWatch alarms, specifically their names and actions. It then filters this list to include only those alarms that have defined actions (i.e., their action field is not null) and outputs each alarm name and its associated actions as plain text strings. The pipe symbol takes the output from the previous command and feeds it into jq, just note. 

Note:

- [Shell scripts best practices _al](https://stackoverflow.com/questions/78497/design-patterns-or-best-practices-for-shell-scripts)

- [How a Linux system boots up, from the power button being pressed to the operating system being loaded _vl](https://www.youtube.com/watch?v=XpFsMB6FoOs): 
  - The boot process starts with the BIOS or UEFI, which prepares the computer’s hardware for action.
  - UEFI offers faster boot times and better security features compared to BIOS.
  - The power-on self-test (POST) checks the hardware before fully turning on the system.
  - The boot loader locates the operating system kernel, loads it into memory, and starts running it.
  - Systemd is the parent of all other processes on Linux and handles various tasks to get the system booted and ready to use.

- Vim terminal: Useful commands: 
  - Exiting Vim
    - `:q!`: Exit Vim terminal without saving
    - `:wq!`: Save and exit Vim terminal
  - Editing Files
    - `:%d`: Clear all contents of a file
    - `:set nu`: Add line numbers to the file
  - Navigating Files
    - `gg`: Move to the first line of the file
    - `G`: Move to the last line of the file
    - `gg=G`: Reindent the whole file
    - `gv`: Reselect the last visual selection
    - `^`: Move to the first non-blank character of the line
    - `g_`: Move to the last non-blank character of the line
    - `gf`: Jump to the file name under the cursor
  - Manipulating Text
    - `xp`: Swap characters forward
    - `Xp`: Swap characters backward
    - `yyp`: Duplicate the current line
    - `yapP`: Duplicate the current paragraph
    - `dat`: Delete around an HTML tag, including the tag
    - `dit`: Delete inside an HTML tag, excluding the tag
    - `w`: Move one word to the right
    - `b`: Move one word to the left
    - `dd`: Delete the current line
    - `<<`: Outdent the current line
    - `>>`: Indent the current line
    - `~`: Toggle the case of the current character
    - `gUw`: Uppercase until the end of the word
    - `gUiw`: Uppercase the entire word
    - `gUU`: Uppercase the entire line
    - `gu$`: Lowercase until the end of the line
    - `da"`: Delete the next double-quoted string
    - `+`: Move to the first non-whitespace character of the next line
    - `S`: Delete the current line and go into insert mode
    - `I`: Insert at the beginning of the line
    - `ci"`: Change what's inside the next double-quoted string
    - `ca{`: Change inside the curly braces (try `[`, `(`, etc.)
    - `vaw`: Visually select a word
    - `dap`: Delete the whole paragraph
    - `r`: Replace a character
  - Navigating Changes
    - `[`: Jump to the beginning of the last yanked text
    - `]`: Jump to the end of the last yanked text
    - `g;`: Jump to the last change you made
    - `g,`: Jump back forward through the change list
  - Repeating Commands
    - `&`: Repeat the last substitution on the current line
    - `g&`: Repeat the last substitution on all lines
  - Additional Commands
    - `:%s/old/new/g`: Replace all occurrences of "old" with "new" in the file
    - `u`: Undo the last action
    - `Ctrl+r`: Redo the last undone action
    - `%`: Move to the matching parenthesis, bracket, or brace
    - `*`: Search forward for the word under the cursor
    - `#`: Search backward for the word under the cursor
    - `f{char}`: Move forward to the next occurrence of {char}
    - `F{char}`: Move backward to the previous occurrence of {char}
    - `t{char}`: Move forward until before the next occurrence of {char}
    - `T{char}`: Move backward until before the previous occurrence of {char}
    - `/{pattern}`: Search forward for the {pattern}
    - `?{pattern}`: Search backward for the {pattern}
    - `n`: Repeat the last search in the same direction
    - `N`: Repeat the last search in the opposite direction
    - `Shift + v`: Visual editor mode

- [File descriptors _al](https://stackoverflow.com/questions/5256599/what-are-file-descriptors-explained-in-simple-terms): 
  - In simple words, when you open a file, the operating system creates an entry to represent that file and store the information about that opened file. So if there are 100 files opened in your OS then there will be 100 entries in OS (somewhere in kernel). These entries are represented by integers like (...100, 101, 102....). This entry number is the file descriptor. So it is just an integer number that uniquely represents an opened file for the process. If your process opens 10 files then your Process table will have 10 entries for file descriptors. Similarly, when you open a network socket, it is also represented by an integer and it is called Socket Descriptor.
  - Other way: When you open a file, OS creates a stream to that file and connect that stream to opened file, the descriptor in fact represents that stream. Similarly there are some default streams created by OS. These streams are connected to your terminal instead of files. So when you write something in terminal it goes to stdin stream and OS. And when you write "ls" command on terminal, the OS writes the output to stdout stream. stdout stream is connected to your monitor terminal so you can see the output there.
  - A file descriptor is an opaque handle that is used in the interface between user and kernel space to identify file/socket resources. Therefore, when you use open() or socket() (system calls to interface to the kernel), you are given a file descriptor, which is an integer (it is actually an index into the processes u structure - but that is not important). Therefore, if you want to interface directly with the kernel, using system calls to read(), write(), close() etc. the handle you use is a file descriptor.
  - Standard Files Provided by Unix: Eg:
  
  | Descriptive Name | Short Name | File Number | Description                 |
  |------------------|------------|-------------|----------------------------|
  | Standard In      | stdin      | 0           | Input from the keyboard     |
  | Standard Out     | stdout     | 1           | Output to the console       |
  | Standard Error   | stderr     | 2           | Error output to the console |

- [/Dev/Null in Linux _al](https://www.geeksforgeeks.org/what-is-dev-null-in-linux/): 
  - In the Linux file system, everything is a file or a directory. Even devices are accessed as files. Your hard drive partitions, Pen drive, speakers, for all of these, there exists a file from which these are accessed. Now to understand how devices are accessed as files, think of it in this way: what do we do with a file? We read data from it and write data to it. /dev is a directory that stores all the physical and virtual devices of a Linux system. Physical devices are easy to understand, they are tangible devices like pen-drive, speakers, printers, etc. A Linux system also has virtual devices which act as a device but represent no physical device.
  - /dev/null is a virtual device, which has a special property: Any data written to /dev/null vanishes or disappears. Because of this characteristic, it is also called bitbucket or blackhole.
  - Eg: `echo "helloworld" > /dev/null`; Then if you do: `cat /dev/null`; You won't get any output. 
  - It is mainly used to discard standard output and standard error from an output.

- [Linux Directory Structure _al](https://linuxhandbook.com/linux-directory-structure/)
  - / – The root directory: Everything, all the files and directories, in Linux are located under ‘root’ represented by ‘/’. 
  - /bin – Binaries: The ‘/bin’ directly contains the executable files of many basic shell commands like ls, cp, cd etc. Mostly the programs are in binary format here and accessible by all the users in the Linux system.
  - /dev – Device files: This directory only contains special files, including those relating to the devices. These are virtual files, not physically on the disk. Some interesting examples of these files are:
    - /dev/null: can be sent to destroy any file or string
    - /dev/zero: contains an infinite sequence of 0
    - /dev/random: contains an infinite sequence of random values
  - /etc – Configuration files: The /etc directory contains the core configuration files of the system, use primarily by the administrator and services, such as the password file and networking files. If you need to make changes in system configuration (for example, changing the hostname), the etc folder is where you’ll find the respective files.
  - /usr – User binaries and program data: In ‘/usr’ go all the executable files, libraries, source of most of the system programs. For this reason, most of the files contained therein is readonly (for the normal user)
  - /home – User personal data: Home directory contains personal directories for the users. The home directory contains the user data and user-specific configuration files. As a user, you’ll put your personal files, notes, programs etc in your home directory. When you create a user on your Linux system, it’s a general practice to create a home directory for the user. Suppose your Linux system has two users, Alice and Bob. They’ll have a home directory of their own at locations /home/alice and /home/bob. Do note that Bob won’t have access to /home/alice and vice versa. 
  - /lib – Shared libraries: Libraries are basically codes that can be used by the executable binaries. The /lib directory holds the libraries needed by the binaries in /bin and /sbin directories. Libraries needed by the binaries in the /usr/bin and /usr/sbin are located in the directory /usr/lib.
  - /sbin – System binaries: This is similar to the /bin directory. The only difference is that it contains the binaries that can only be run by root or a sudo user. You can think of the ‘s’ in ‘sbin’ as super or sudo.
  - /tmp – Temporary files: As the name suggests, this directory holds temporary files. Many applications use this directory to store temporary files. Even you can use directory to store temporary files. But do note that the contents of the /tmp directories are deleted when your system restarts. Some Linux system also delete files old files automatically so don’t store anything important here.
  - /var – Variable data files: Var, short for variable, is where programs store runtime information like system logging, user tracking, caches, and other files that system programs create and manage. The files stored here are NOT cleaned automatically and hence it provides a good place for system administrators to look for information about their system behavior. For example, if you want to check the login history in your Linux system, just check the content of the file in /var/log/wtmp.
  - /boot – Boot files: The ‘/boot’ directory contains the files of the kernel and boot image, in addition to LILO and Grub. It is often advisable that the directory resides in a partition at the beginning of the disc.
  - /proc – Process and kernel files: The ‘/proc’ directory contains the information about currently running processes and kernel parameters. The content of the proc directory is used by a number of tools to get runtime system information. For example, if you want to check processor information in Linux, you can simply refer to the file /proc/cpuinfo. You want to check memory usage of your Linux system, just look at the content of /proc/meminfo file.
  - /opt – Optional software: Traditionally, the /opt directory is used for installing/storing the files of third-party applications that are not available from the distribution’s repository. The normal practice is to keep the software code in opt and then link the binary file in the /bin directory so that all the users can run it.
  - /root – The home directory of the root: There is /root directory as well and it works as the home directory of the root user. So instead of /home/root, the home of root is located at /root. Do not confuse it with the root directory (/).
  - /media – Mount point for removable media: When you connect a removable media such as USB disk, SD card or DVD, a directory is automatically created under the /media directory for them. You can access the content of the removable media from this directory.
  - /mnt – Mount directory: This is similar to the /media directory but instead of automatically mounting the removable media, mnt is used by system administrators to manually mount a filesystem.
  - /srv – Service data: The /srv directory contains data for services provided by the system. For example, if you run a HTTP server, it’s a good practice to store the website data in the /srv directory.

- 

- 


----------------------------------------------------------------------

