
# Linux_internals_and_commands


- `grep -i "UNix" geekfile.txt`: Case insensitive search
- `grep -c "unix" geekfile.txt`: Displaying the count of number of matches
- `grep -l "unix" *` (or) `grep -l "unix" f1.txt f2.txt f3.xt f4.txt`: Display the file names that matches the pattern
- `grep -w "unix" geekfile.txt`: Checking for the whole words in a file
- `cat <file_name>`: View file content
- `:q!`: Exit vim terminal 
- `:wq!`: Save and exit vim terminal 
- `:%d`: Clear all contents of a file 
- `:set nu`: Will put index numbers in file opened via vim
- `vi ~/.bash_profile`: Opens the .bash_profile file in the vi text editor. This file typically contains settings and configurations for the Bash shell.
- `vi .bash_history`: Opens the .bash_history file in the vi text editor. This file contains a history of commands that have been executed in the current user's Bash shell.
- `top`: The top command displays real-time information about system processes. It provides a dynamic view of system resource usage, including CPU and memory usage, as well as information about running processes. Users can monitor the processes, their resource consumption, and manage them interactively.
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
- `set | grep AWS_KEY`: Displays environment variables (set) and filters the output to show lines containing AWS_KEY using grep.
- `screen -ls`: Lists currently running screen sessions.
- `screen -S vikas`: Starts a new screen session with the name vikas.
- `find ~ -name aws_credentials`: Searches for files named aws_credentials in the user's home directory (~).
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

Note: [Shell scripts best practices _al](https://stackoverflow.com/questions/78497/design-patterns-or-best-practices-for-shell-scripts)

- [How a Linux system boots up, from the power button being pressed to the operating system being loaded _vl](https://www.youtube.com/watch?v=XpFsMB6FoOs): 
  - The boot process starts with the BIOS or UEFI, which prepares the computer’s hardware for action.
  - UEFI offers faster boot times and better security features compared to BIOS.
  - The power-on self-test (POST) checks the hardware before fully turning on the system.
  - The boot loader locates the operating system kernel, loads it into memory, and starts running it.
  - Systemd is the parent of all other processes on Linux and handles various tasks to get the system booted and ready to use.

----------------------------------------------------------------------





















