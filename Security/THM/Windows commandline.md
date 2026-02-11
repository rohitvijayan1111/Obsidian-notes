
# COMMANDS
## Basic
- `set` to check your path from the command line.
- `ver` command to determine the operating system (OS) version
- systeminfo ->command to list various information about the system such as OS information, system details, processor and memory. The terminal below shows a snippet of the displayed output.
## Network commands

- ipconfig
- ipconfig /all
- ping 
``` nslookup <domainname> / nslookup <domainname> <name server ip>``` searches for the ip address of the domain (if name server ip is given then it searches in that server.) 
- `tracert target_name` traces the network route traversed to reach the target. (exploits TLL to find the intermediates)
- `netstat`. This command displays current network connections and listening ports.


# File management commands

- dir - prints the working directory (/a - all files(including system files) /s - all files in the current and subdirectory.)
- `tree` to visually represent the child directories and subdirectories.
- cd target_directory
- To create a directory, use `mkdir directory_name`;
- o delete a directory, use `rmdir directory_name`
-  You can easily view text files with the command `type`.
- you can move files using the `move` command
- we can delete a file using `del` or `erase`.

## Task and process management
- We can list the running processes using `tasklist`
- search for tasks related to `sshd.exe`, we can do that with the command 
  `tasklist /FI "imagename eq sshd.exe"`. Note that `/FI` is used to set the filter _image name equals_ `sshd.exe`.
- With the process ID (PID) known, we can terminate any task using `taskkill /PID target_pid`

- `chkdsk`: checks the file system and disk volumes for errors and bad sectors.
- `driverquery`: displays a list of installed device drivers.
- it is equally important to know that `/?` can be used with most commands to display a help page.