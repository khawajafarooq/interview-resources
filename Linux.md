##Linux

- http://linux-training.be/linuxfun.pdf
- Video training: https://prod-edx-mktg-edit.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-0

- FILES NAMES ARE CASE SENSITIVE
- Everything on Linux is a FILE. Files, processes, folders, HD partitions etc

#####Linux vs Unix
Linux is a clone of Unix. Unix OS normally comes from a single vendor.
Linux is just a kernel. All Linux distributions includes GUI system + GNU utilities (such as cp, mv, ls,date, bash etc) + installation & management tools + GNU c/c++ Compilers + Editors (vi) + and various applications (such as OpenOffice, Firefox). However, most UNIX operating systems are considered as a complete operating system as everything come from a single source or vendor.


####PDF -> Page 82
- man command_name -> details of a command
- whatis command_name -> returns all the commands that match the specific keyword. Each command also contains its description.

#### PDF -> Page 84 -> Directories
- ls -lh -> Shows the list of files/folders in a directory with all the information but the filze size is more human readable with KB/MBs.
- mkdir -p foldername -> example mkdir -p A/B/C, now if A and B do not exist then -p will create those folders.
- rmdir -p foldername -> same as above. recursivly delete folders (only if they are empty).
- ls /folder1 /folder2 -> lists all the files in both folders at once
- file file_path -> tell the type of file.
- head/tail -n [number] [file_path] -> shows specific number of lines from head/tail.
- cat -n [file_path] -> shows the complete file with line number before each line.
- cat file1 file2 -> shows the content of both files
- cat file1 file2 > file3 -> creates a new file with the content of both
- cat > file4 -> opens an editor to write text directly and CTRL+D to write the file and end.

####File System
Binaries are  files  that  contain  compiled  source  code  (or  machine  code). In Linux/Unix, they are placed in /bin or /sbin. They are executable on the computer. /bin contains user binaries. These are the executables that user can use to perform different tasks like cd,pwd etc. /sbin binaries are used to manupulate the operating system.
- /lib is contains all the shared libraries that are used by the executables.
- /opt is used to store optional softwares. External softwares like hadoop etc
- /boot contains all the files needed to boot a computer.
- /etc all the machine specific configuration files are stored here.
- /home users personal space. Can store anything.
- /root storage place for data of root user.
- /tmp is used to store temporary data.
- /var files that are unpredictable like log files are placed in this directory.

- alias [alias_string]=[command in single quotes] -> example: alias rm='rm -i'  to enable interactive menu for always avoid deleting without confirming.
- & -> When a line ends with an ampersand & , the shell will not wait for the command to finish. You will get your shell prompt back, and the command is executed in background. You will get a message when this command has finished executing in background.
- && (logical AND) -> example echo first && echo second -> If the first one succeeds only then the second one is executed.
- || (logical OR) -> example echo first || echo second -> second command will only be executed if the first one fails.

