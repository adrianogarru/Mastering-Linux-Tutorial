## Linux file System

The linux file system follows a tree-like structure.
Everything can be traced back to the **"/"** directory.
Root users have the highest privileges in the system.
**/home** directory store the directory (folders) of each user present in the system.
**/root** is the home directory for the root user.

**/** = It is the upper level of directory structure is the root where we can see the below directory:

- **bin** Contains executable file for basic command like cp ls.
- **boot** Contains the static bootloader and kernel executable and configuration files required to boot a Linux Computer.
- **dev** Contains the file from device hardware attached to the system but there are NOT files related to the driver.
- **etc** Core system configuration directory, should hold only configuration files and not any binaries.
- **home** Storage the file of each user in the system, each user has his/her folder. 
- **media** Place to mount external device such a USB pen.
- **mnt** Temporary mount point for regular file systems, it used to make the file system available in the system, should never be used to install others software.
- **opt** Optional files such as vendor supplied application programs should be located here.
- **sbin** System binary files. These are executables used for system administration.
- **temp** Used by the operating system and many programs to store temporary files.
- **usr** These are shareable, read-only files, including executable binaries and libraries, man files, and other types of documentation.
- **var** Variable data files are stored here. This can include things like log files, MySQL, and other database files, web server data files, email inboxes, and much more.

---------------------------------------------------------

### Navigating the File System

Commands:

- **pwd** -> Where we are currently. (Print working directory).
- **ls** -> List files and directory, only ls show file directory where we are.
 - **ls /path** -> example **ls /home** list files and folders in home directory.
 - **ls -F** -> Classified the files folder, to recognize what is folder or file, folder will have a slash **/** after the name.
 - **ls -l** -> This puts everything in long format with many information, file permission - group - user where belong - size - last editing.
 - **ls -lh** -> **"h"** option is for "human reading", the size of the file will be more understable.
 - **ls -a** -> Show hidden files or directory, these start with a full stop.
- Full stop **.** or double **..**, 1 full stop represent current folder and **..** the previous (It can use to navigate with command cd, example **cd ..** to go to directory above).

- **cd** -> Basic command used to navigate in the folder. (by default if you execute only **cd** you will move to the previous directory).
 - **cd foldername** -> Example "**cd home**" to move inside a specific folder (**Relative Path**).
 - **cd /directory** -> The **/** is to **"absolute"** and it is used to access to a directory not located in our path (example you are in home and you want to access to var) **cd /var**
 - **cd /directory/folder** -> It is possible to concatenate to access more fast in a specific folder in the dir example: **cd /var/log**
 - **cd /** -> To move direct to a top root directory.
 - **cd ..** -> Move up to directory.

*Shortcut
- **TAB** to complete automatically a path or file name.

**Relative** and **Absolute** path, this is important concept to understand in how to move across directory, a relative path is a folder present in the path where we are (**pwd** to check).
and absolute is a file folder located in different parth where we are located.
- When navigation is in absolute way, it is better to refer to main directory in the file Linux system (var etc media etc).

----------------------------------------------------------------

### File Extension in Linux

In Linux, the file extension does not matter, because Linux will check inside the file to determinate the type.
It can be important in the UI to open the file in the proper software.
In case an extension file does not exist the system will recognize the structure inside a will open a file in base the program that matches.

Commands
- **file [filename]** -> To get the file type example file data.txt

----------------------------------------------------------------

### Wildcards

It is useful to perform many actions in multiple file/folder in the system by building a pattern called regular expression.

- * (star) Match anything regardless of length
- ? Match a single character.
- [] Match to specify a range.

In the command line via argument it is possible to create a pattern that should match to a specific instruction.

Example

1. Commands based on **.*.**

- **ls folder/ folder2/** -> Example **ls /home/ /var/ /etc/** --> list a specific file in specified directory.
- **ls** * --> will list everything plus directory below, example if run from root / will list the file folder inside the main folder just down root
- **ls (letter)* -> example -ls a* will match all the files that start with a.
- **ls *(letter)** -> example -ls *.txt will match all the file end with .txt (It will be good to list file with a specific extension)

2. Commands based on ?
- **ls letter?letter** -> example -ls a?t will match a file with file name length 3, so a file that start with a and finish with t
--ls a??t -> in this case is a file with length of 4, so each ? Meaning a space.

3. Commands based on **[ ]**

- ls [letter-letter]* -> example ls [a - g]* it will filter only file names starting with a letter between a and g.
- ls *[number..number]* -> example ls *[0..9]* it will filter only file names that contain a number.
- ls [letters]* -> example ls [daiedg]* it will filter file names that contain at least 1 of these letters.
- ls [!letters]* -> example ls [!atred]* it will trigger only the files that do not start with one of letter atred

--------------------------------------------------------

### Creating Files and Directory

commands:

- **touch** -> Create a file
- **mkdir** -> create a folder
 - **mkdir -p** -> Create a path folder
 - If a folder has a space, the name should be included in the quotes, best practice is to not use a space but underscore _

---------------------------------------------------------

### Brace expression

It is a powerful way to create with a single command line a multiple folder or file or to perform action inside of it.

- **mkdir {namefolder1,namefolder2}** -> It will create new folders.
 - let's suppose each folder name should be addressed with a number or specific letter, example folder with month name and year.
 - **mkdir {jan,feb,march,apr,may,june}_{2020,2021}** in this way will create months folder with respective year.

Let's suppose that each of this file need to have a file inside

- **touch {foldername,..}/filename**
-- Example: **touch {jan,feb,march,apr,may,june}_{2020,2021}/list.txt**

Now if is needed to check that all the file are really created, it is possible to apply this brace expression even to ls command

- **ls {jan,feb,march,apr,may,june}_{2020,2021}**

---------------------------------------------------------

### Delete files        

Commands

- **rm (filename)** -> Example rm filename
- **rm /foldername/filetodelete** -> if you need to delete a file in a different path where they are located.
- It is possible to delete many files in the same time, **rm file1 file2**

### Remove file with wildcard

Example commands

- **rm *txt** -> it will remove file that have everything in the end that match with our text, example file with a particular extension **rm *.txt**
- rm txt* -> In this case it will remove file that start with the letters indicated
- rm *textornumber* -> In this case it will delete a file that contains a letter or number.
- rm *[txt or number]* In this case we can provide a number range o multiple specific parameter

### Delete Folder

- **rm -r** -> Folder name
 - This command will delete the folder included all that is inside, it should be used very carefully!
 - **rm -ri** -> with this command before to start to delete, system will interact and ask a permission to continue to each folder
 - **rmdir** -> It will allow only to remove empty folders.

### Copy File

- **cp (filename) (nameofcopy)** -> Example **cp index.html copyofindiex.html**
- **cp (filename) /folder/copiedfile -> cp index /storage/copyofIndex**

### wildcard on copy

- **cp folder/* .** -> copy everything in the folder and passed in our currently location in the shell
 - The full stop mean current location a double full stop the directory above where we are located.

copy folder itself

- **cp -r** -> example **cp -r namefolder/ /folder** where to copy this command will copy all the folder.

### Moving and Renaming Files

The command mv its used for rename and moving

- **mv filename newfilename**
- **mv foldername new foldername**
- **mv folder/folder* .** -> Move a folder to our current operation path
- **mv folder/ /folder** -> Move folder /folder where is needed.
- **mv folder/ ./newname_of_folder** -> Change the name of the folder

---------------------------------------------------------

### Nano

I used in my tutorial GNU Nano 2.9.8 in Amazon Linux VM, it can change a bit across version.

Command

**nano namefile** -> Create a new txt file and start to edit.
**sudo nano namefile** -> In case command are run with not admin privileges, privileges are required to edit particular file like system files.

In the bottom there are the commands present in Nano file editing, in order to start a command should be press **CTRL + letter**
- Some function can be disabled but it is possible to enable in the "nano file system", usually located **etc/nanorc**
- In order to allow a function or disable, the # make the difference, if it is placed before the function is disabled if is not the function is enabled.

**nano file** -> Start to modify
Relevant key combination to nano:

- **CTRL + G or F1** -> Get help, it is possible to figure out all the commands that are included in nano
- **CTRL + X or F2** -> It is you exit, in case of change, system will ask to save the changes or not plus possibility to edit filename
- **CTRL + O or F3** -> It will save it automatically without confirmation.
- **CTRL + W or F6** -> To find a specific statement in the file, example file system where you need to change some value.

- **ALT + U** -> To undo -> Example, by mistake something has been deleted.
- **ALT + M** -> To enable the mouse cursor in the terminal.

---------------------------------------------------------

### Locate

This command works based on the "local file database" where are registered the files of the system

- Database is updated once per day, this means that what happen in the meantime is not updated straight forward.
- It is case sensitive
--sudo updatedb -> Update the system database where locate is looking for, the sudo is the main command to use to run action connect to system administrator if is only 
ran updatedb it will not work.

commands example:

- **locate *.conf** -> In this case will find any file that match with the end .conf
- **locate *.CONF** -> In this case will not find anything, Linux is case sensitive.
 - **locate -i *Conf** -> If you use a -i it will ignore the case type.
 - **locate -i --limit 3 *.conf** -> It is to limit to 3 results the list of found
 - **locate -S** -> Information about the database of the system.
 - **locate -e *.conf** -> It will check 'e' if the file exist before to show the result.
 - **locate -e --follow *.conf**-> Follow option is used to understand if the path is really existing and return what it show

---------------------------------------------------------

### Find

Instead of locate command, it does not refer to the database and it is a bit slower than locate.

Commands:

- **find** -> If executed it will list all files in the directory where you are located and the others in the below.
- **find /** -> If executed it will list all the file present in the system, remember that **"/"** mean top level directory root.
- **find /foldername** -> It will list all the files from a specific folder.
- **find -maxdepth 2** -> It will look at the files in the current folder if you set 3 it will go down to another level.
- **find -type f** -> It will find and filter only the file.
- **find -type d** -> It will find and filter only the folder.
- **find -maxdepth 2 -type f** -> It is possible to combine **"maxdepth"** with "file type" but **"maxdepth"** should be use first
- **find -name "filename"** -> It will looking for to that particular file name in the directory where we are running the command
 - **find -name "*.txt"** -> It is possible to apply Wildcard on the filename, keep in mind the brace expansion [] is not working.
 - **find -iname "FILENAME"** ->The option **-iname** it is used to ignore the lowercase or uppercase and just focus on characters.
 - Important! in case command should be run to all system commands find should start with find **/**
- **find / -type f -size +100k** -> It is used to find all file with size greater than 100k (in this example) but its possible to adjust to our requirement
 - **sudo find / -type f -size +100k** ->Sudo will allow to find and access even to system files that need root privileges.
 - **sudo find / -type f -size +100k | wc -l** -> Option **wc -l** in pipeline will show the number of the file present
 - **sudo find / -type f -size +100k -size -5M** -> Adding another size value its is possible to create a size range to look for
 - **sudo find / -type f -size -100k -o -size +5M** ->Adding -o is a conditional format mean "OR" so in this case or less than 100k or higher than 5M

- **sudo find / -type f -size +10M -size -50M -exec cp {} ~/copy_files \;** -> In this expression with option **"-exec"** it is possible to concatenate the find command to another action in this case **"cp"** in specific folder.
- **sudo find / -type f -size +10M -size -50M -ok cp {} ~/copy_files \;** -> Instead of exec, the **-ok** option need an explicitly approval to continue with the task in this case if copy or not.

- **find -type f -name 'findme.txt' -exec mv {} /folder \;** -> Instead of copy it is possible to use a move command too.

---------------------------------------------------------

### View File and Manipulate contents

- **cat** -> It can be use to print the file on the terminal, to concatenate and print multiple file and we can even redirect multime file in a single one
 - **cat file1 file2 file3 >> mainfile**

- **tac** -> It is like cat but it shows the data in reverse mode.

- **rev** -> It revert horizontally the text file

It is possible to pipe this command like: **cat file1 file2 file3 | tac**

- **less filename** -> Instead of cat it will only open a portion of the file and allow it to scroll with arrows key and make it easy to read.
- It can be a concatenation with cat, example **cat filename | less**
- It is possible to concatenate **cat** with **"|"** **"head"** it will show by default not more than 10 line
- **head -n 5** -> Option "n" in "head" will allow showing only the determinate number of line in this case only 5
- **tail** -> It is the opposite than "head", it will start to show from the bottom of the file and with **"-n"** option line in head it is possible to determinate how many lines to show.

---------------------------------------------------------


### Sorting data

- **sort filename** -> It will sort out alphabetical.
- **sort** Can be concatenated with other option:
- **tac** -> Reverse example **sort filename | tac**
- **less** -> to show less result.
- **sort -r** -> In sort there is even the option included without use pipeline.
 -*sort does not work by default with the number for this is need the option "-n" example "**sort -n filename**" (that contains number).
- **sort -n -u** -> **"u"** option will give you the unique value.
- **sort -k** -> **"k"** option is a key definition, example **ls -lh | sort -k 5n** in this case will be used the 5th column of the table as a refer point to sort out
- In case sort out of months is needed, the option capital letter **M** is used for this purpose.

---------------------------------------------------------

### Grep

It is used to filter out only the data string that we needed, or we want to exclude in a file or in folder

- **grep stringneeded filename** -> Example grep e filename.txt in this case only letter **'e'** will be highlight.
- **grep -c stringeeded filename** -> The option **c** will tell in how many rows there is the string we are looking for.
- **grep -i stringneeded filename** -> The option **-i** will run the command in not in case-sensitive.
- **grep -ic stringneeded filename** -> It is possible to concatenate the option.
- **grep -v stringneeded filename** -> In this case option **-v** will show strings that are not matching from the string set.

- **grep stringneeded filename1 filename2** -> It is possible to compare the match across 2 files and so on

- **grep** can be used to find a file by name, suppose in a folder is needed to find a specific file name, follow command:
- **ls | grep filename** -> It in bases of the file directory listed will highlight what is looking for.
-  **ls -lF / grep root** -> In this example is possible to have only the folder with root privileges
-  **ls -lF / | grep -v /** -> In this example it is possible to have only a file instead of directory because / in the end of the name mean directory
- **man k print | grep files** -> In this example it is possible to filter out the manual in base of keywords needed.

---------------------------------------------------------

### File Archiving and Compression

**Tarballs** **tar** are container to store files in for **compression**
As indicate before Linux does not care of the extension but for best practice it is better to indicate if file is tar and the type of compression.

### Archive

- **tar -cvf nameofarchive file1 file2 file3 etc** -> Basic command to compress/archive files.
- **c** -> Option to compress.
- **v** -> Option to let us inform on the process, good practice to use.
- **f** -> Option to accepts files.
 - Instead of file it is possible to apply it with entire folder, example: **tar -cvf nameofarchive foldername**
- **tar -tf namearchive** -> It will not extract but shot the file inside of the archive.
- **tar tvfw namearchive** ->Verify archive without extract and gathering info on the file inside.
- **tar -xcf nameofarchive** -> It will extract the files.
- **tar -rvf nameofarchive filetoadd** -> Option **r** will allow to add an existing archive file or directory.

### Compression

There are 2 types, one is gzip that is faster and good to compress files/folder not so big the other is bzip2 that issl sower but more effective especially with files with big size like video.

- **gzip archivenae** -> To zip compress the file.
- **gunzip zipedarchived** -> To unzip the file.

- **bzip2 archivenae**  -> Compress archive.
- **bunzip2 zipedarchived** -> Uncompress archive.

It is possible to make a zip file compatible example with Windows OS.

- **zip archivename file1 file2 etc..** -> This will compress in zip format that will be readable for OS Windows
- **unzip archivename** -> To unzip the files

The archive and compression can be combined in one row command.

### Archive and compress in one row with gzip

- **tar -cvzf namearchive.tar.gz file1 file2 etc** -> With option **z** it indicated the **gzip**.
- **tar -xvzf namearchive.tar.gz** -> This command will extrac the files, **x** is the option to extrac and **z** is from **gzip**.

### Archive and compress in one row with bzip2

- **tar -cvjf namearchive.tar.gz file1 file2 etc** -> Option **j** refer to bzip.
- **tar -xvjf namearchive.tar.gz** -> Option **x** is to extract.
