
# Linux_internals_and_commands


- `grep -i "UNix" geekfile.txt`: Case insensitive search
- `grep -c "unix" geekfile.txt`: Displaying the count of number of matches
- `grep -l "unix" *` (or) `grep -l "unix" f1.txt f2.txt f3.xt f4.txt`: Display the file names that matches the pattern
- `grep -w "unix" geekfile.txt`: Checking for the whole words in a file
- `cat <file_name>`: View file content
- Vim terminal: 
  - `:q!`: Exit vim terminal 
  - `:wq!`: Save and exit vim terminal 
  - `:%d`: Clear all contents of a file 
  - `:set nu`: Will put index numbers in file opened via vim
  - `vi ~/.bash_profile`: Opens the .bash_profile file in the vi text editor. This file typically contains settings and configurations for the Bash shell.
  - `vi .bash_history`: Opens the .bash_history file in the vi text editor. This file contains a history of commands that have been executed in the current user's Bash shell.
- `fdisk -l`: The fdisk command is used for disk partitioning and disk management on Unix-like systems. The -l option lists information about all available disks and their partitions. This command is typically used to view the current disk layout and partitioning scheme of the system.
- `ps -ef`: The ps command is used to display information about running processes on Unix-like systems. The -ef options stand for "everyone" (-e) and "full-format" (-f), which together instruct ps to display information about all processes in a detailed format. This includes information such as the process ID (PID), the terminal associated with the process, the user running the process, CPU and memory usage, and the command being executed.
- `ls -l <dir path else it lists current path files>`: Lists files and directories in the specified directory (or the current directory if none is specified) with detailed information, including permissions, ownership, size, and modification date.
- `ls -lrt`: Lists files and directories in the current directory in long format (-l) sorted by modification time in reverse order (-r for reverse, -t for time).
- `pwd`: Prints the current working directory.
- `ls -la`: Lists all files (including hidden files) and directories in the current directory in long format, showing detailed information, including hidden files (-a for all).
- `su`: Allows switching to another user account. If no username is specified, it defaults to the superuser (root) account.
- `su root`: Switches to the root user account.
- `whoami`: Displays the username of the current user.
- `which python`: Displays path where executable file of python is located.
- `top`: Displays real-time information about system processes, including CPU and memory usage.
  - In your keyboard if you press button 'c' after running top command - it will display the stats in detailed manner. 
- `set | grep AWS_KEY`: Displays environment variables (set) and filters the output to show lines containing AWS_KEY using grep.
- `screen -ls`: Lists currently running screen sessions. screen command in Linux provides the ability to launch and use multiple shell sessions from a single ssh session.
- `screen -S vikas`: Starts a new screen session with the name vikas.
- `find ~ -name aws_credentials`: Searches for files named aws_credentials in the user's home directory (~).
  - `find / -name "requirements.txt" 2>/dev/null`: Searches for file from root directory. The /dev/null command suppresses error messages about directories you don't have permission to read.
  - `find . -name "requirements.txt"`: Command will search for the file starting from the current directory (.) and look through all subdirectories.
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
- `du -sh * | sort -h`: Displays the disk usage of all files and directories in the current directory in a human-readable format, summarizes the total, and sorts the output numerically and in a human-readable way (-h).
- `conda list`: Lists installed packages and their versions using Conda, a package manager for Python.
- `echo $PATH`: It prints out the value of the PATH environment variable. 
- `sudo -su user`: It is short for sudo -s -u user. The -s option means to run the shell specified in the environment variable SHELL if this has been set, or else the user's login shell. The -u user option means to run the command as the specified user rather than root. 
- `sudo su user`: It will use sudo to run the command su user as the root user. The su command will then invoke the login shell of the specified username. The su user command could be run without the use of sudo, but by running it as root it will not require the password of the target user.
- `rm /path/to/directory/*`: To remove all non-hidden files* in a directory 
- `rm -r /path/to/directory/*`: To remove all non-hidden files and sub-directories (along with all of their contents) in a directory
- `rm -rf "/path/to the/directory/"*`: Force removal of files
- `tail -f /var/log/syslog`: It only shows the last part of the logs, where problems usually lie. tail will continue watching the log file and print out the next line written to the file.
- `history`: Provides a chronological list of previously executed commands
- `bash`: bash is a command interpreter, a shell, a program with an interface that interprets the commands that you put into it.
- `pstree`: To know how many sub-shells deep you are. 
- `netstat`: The network statistics command is a networking tool used for troubleshooting and configuration, that can also serve as a monitoring tool for connections over the network.
- `ps aux`: Similar to `ps -ef`. Displays information about running processes. 
- `last`: This command in Linux is used to display the history of last logged in users.
- `ssh -i`: To ssh into a machine. '-i' is identity_file which selects a file from which the identity (private key) for public key authentication is read. 
- `ping -c 1 $(hostname)`: To get IP address of the machine
- 

who
last
cmp <> <> 
cp <> <>
sh test_file.sh 

chmod a+x test_file.sh - a+x means
chmod a-x test_file.sh - a-x means 

sudo apt-get install iftop
sudo dmesg
clear
sudo kill -9 335793
date
sudo ls -l /proc/330046/fd/1 or 2 or 3 

cd /proc/324049 -> then tail -f fd

cat  /home/circleci/etl-pipes/deploy/ansible/roles/simpl_lib/tasks/main.yml | head -88 | tail -1

vim :set nu, 
other vim commands also keep a track

Note: [Shell scripts best practices _al](https://stackoverflow.com/questions/78497/design-patterns-or-best-practices-for-shell-scripts)

- [How a Linux system boots up, from the power button being pressed to the operating system being loaded _vl](https://www.youtube.com/watch?v=XpFsMB6FoOs): 
  - The boot process starts with the BIOS or UEFI, which prepares the computer’s hardware for action.
  - UEFI offers faster boot times and better security features compared to BIOS.
  - The power-on self-test (POST) checks the hardware before fully turning on the system.
  - The boot loader locates the operating system kernel, loads it into memory, and starts running it.
  - Systemd is the parent of all other processes on Linux and handles various tasks to get the system booted and ready to use.

- [How to get process details from its PID](https://stackoverflow.com/questions/29105448/get-process-info-from-proc)
  - To get this info: `cd /proc` in the linux machine then: 
  - ```
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
    etc etc... (check hyperlink)
    ``` 

----------------------------------------------------------------------

