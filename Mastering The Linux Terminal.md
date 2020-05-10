## Mastaring The linux Terminal

### Understanding Command structure

comand-name [option] [input]

- Not all the comand name needs an option / input example date (can be run without additional input)
- Option is called operand
- It is possible to use a short option, example: **date -u or long date --universal**
- CommandNames need to be on the shell search path

---------------------------------------------------------

### Difference: Commands(terminal) and the Shell

- Commands is case-sensitive.
- Commands are the "text command line" The shell is interpreting the commands line
- Terminal is the access to the shell to give input commands.

Bash Shell is shell to programming purpose.

The commands are consider like a little programs that perform action and have own
behavior.

---------------------------------------------------------

### Some Commands

- **echo** -> print a word in terminal
- **cal** -> calendar
- **date** -> date of today
- **clear** ->clean the shellecho (shortcut: CTRL + L)
- **history**: ->history of ran commands
- **-!(number of commands)** you can run a previous command
- **!!** to run the last commands
- **history -c; history -w** clean commands history and with -w remove permanent 
- **exit** -> to close the terminal CTRL + L)
- **which [commands name]** -> Indicate the path where is stored the file program of the command.

---------------------------------------------------------

**echo $PATH** -> PATH it is a unix variable that indicate where executable files are located in the directory
in this case, the command echo + print show the directory where file are executed

**Which [commands name]** Path where is stored the file program of the command.

---------------------------------------------------------

### The manual page

It's the main manual of the system structured in 8 sections.

1. Section **User commands** - Run from each privileges.

2. Section **System calls** - Contains Program Function to make a call to the Linux Kernel, it is
low level part of the operative system, it is pretty advance.

3. Section **C Library Function** - Access to specific thing, as graphical, user interface is most for who
program on C.

4. Section **Devices and Special files** Reletated to device, example USB ports CD Driver.

5. Section **File Formats and Conventions** Related to file formats and convention of files in the computer for some customized
on file structure.

6. Section **Games** Related to game installed on the PC as a special commands.

7. Section **Miscellaneous** uncategorized stuffs, as protocol or file system to have info about those.

8. Section **System Administration** all the stuff related to system administrator, it required privileges to run those functions of those commands
it is related to users administration, passwords, automatization and advance stuff.

Commands:

- **man -k(search function) (what we are looking for)** example **man -k which**
   - It will show the list about info find related to search term and in () the section of man

- **man (section) (term)**: In order to open a manual page example man 1 which
  - If its in section 1 you do not need to add it

**man -k "search contents you need"** To search a specific topic example **man -k "list directory contents"**

**Help** Get list of all commands

**help (command)** Get a specific help for one commands example **help cd**

---------------------------------------------------------

### Input Output Standard data stream

1 Data stream for input and 2 ways to get data out

Standard Input (0) (stdin): This accept text as input and processed by the shell.
Standar Output (1) (stdout): Successfully (input) return back to the terminal.
Standard Error (2) (stderr): Related to not successful input and return error log.

*The number in the brackets are "File descriptor" is a number that uniquely identifies
an open files on computer and description the data resource, in case below associate to data stream.

Standard input (0) ------> Command --------> Standard Output (1)
Command Arguments ------> [_____________> Standard Error (2)

Commands in base of his function can have argument, are values used to provide specific info or instruction.
Example command: **ls** -> Give a list of directory **ls -l** the argument **-l** will return the list in vertical way.

Not all command accept standard input
Example command: **echo**


------------------------------------------------------------------------

### Redirection

It is a feature in Linux that when you execute a command it will change the standard
input/output.

command **cat** used to concatenate or stick multiple files

**cat** is good example because he read from standard input (terminal) and output in the terminal too.

###### Redirect standard output to a file **cat 1> output.txt**
- *Number is connected to the type of stream 1 (output) in this case will work even without number of file destination.
  -What we will write on the terminal will be saved in file called output.txt.
  - Redirecton in case in a new command session will delete what write before
    - To solve and not overwrite the file is needed to add another >: cat >> output.txt
     - This symbols (2) >> appending to file > will overwrite the file.

###### Redirect standard error **cat -k bla 2> error.txt** (cat trigger error with -k)
*Number 2 is connect to the data stream error

###### Redirect standard error and output in one line: **cat > output.txt 2>error.txt**
 - In this case output file does not need a number file descriptor but error string need it
 - In this scenario if there are not error result will me save in output.txt if will be error in error.txt

###### Redirect standard input **cat < input.txt**
- It is possible to create a file with **cat > input.txt**

- Call it with cat < input.txt

Some concatenations read from input.txt and save text.txt
 - cat 0< input.txt 1> hello.txt

Example:

command **tty**: it show where terminal is located
 - Open a second terminal and check the path, this path will be used to print message on the second terminal from the 1st
 - **cat 0< input.txt > /dev/pts/1** 

---------------------------------------------------------

### Piping

Connect standard input to one command to another one.

Save in file the result from date commands:
- **date > date.txt**

Commands **Cut**, it will take part of the text in base of rule applied and print out

Example:

1. Save a date in the file: **date > date.txt**
2. Print out only one part: **cut < date.txt -d ' ' -f 1**
  - cut < date.txt it's the part that is going to read and -d -f are the option to trigger the value desired
  - In the command above -d =delimiter (rule to apply how to split a file ' ' in these case is space -f is field 1 - 2 and so on
  - In order to get the argument for command cut, use commands man cut

Above the commands read on the file (2 steps) below its possible to pipeline
commands: **date | cut -d ' ' -f 1**
 - It will directly print out the field required
 - Experiment save this input in file just adding > date | cut -d ' ' -f 1 > file.txt
 - pipeline | is used to distinguish and concatenate the different commands.


---------------------------------------------------------

### Advance Piping Techniques

**Tee** commands for flow the data in 2 directions to standard input and a file


Example on use tee command
Commands: **date | tee file.txt | cut -d ' ' -f 1**
 - **Tee** will save in file we declared after the command
 - **cut** will only show on screen in output the part of data needed
    - If we set command file in the end like here:  **date | cut -d ' ' -f 1 | tee fulldate1.txt** it will save in file the part of data wanted.
    - Save full data and a part:  **date | cut -d ' ' -f 1 | tee fulldate1.txt > today.txt**  (with **>** in the end, saved only a part we cut off)

---------------------------------------------------------

### xargs commands

**echo** does not accept standard input, so to print in standard output use **xargs**

Example delete file listed in one txt file
1. Create a file with name file to delete
2. The file contains the list will be called by **cat < filetodelete.txt**
   - Cat will just open the file and show the list
   - If we pipe cat with rm example **cat < filetodelete.txt | rm**
     -It will **NOT** work because the file print in the terminal are not standard output
   - **xargs** its used to make this text as a standard output in the terminal in this way rm command can proceed to remove it
  - Final command **cat < filetodelete.txt | xargs rm**
     - In case you run again it will trigger error because file is already deleted.

---------------------------------------------------------

### Aliases

Aliasies is a custom command that you can set, usually used to recall a pipeline code you created with only one custom command.

Exampe: **alias getdate='date | tee /home/ec2-user/fulldate.txt | cut -d " " -f 1 | tee /home/ec2-user/shortdate.txt | xargs echo hello'**
- alias 'getdate' is the name of the custom command
- In the quotes ' ' the pipeline command we want to be executed
- I use an Amazon virtual instance end my code should be located in file **.bashrc** 
   - Once the alias has been created is needed to open a new terminal
   - In case of remote access via commands: **reset** or **tset**
































 












































































