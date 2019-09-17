# Commands for the List of Animals

A new directory should be created and then a new file created to start a piped command. Here we will make the file about wild animals
wildanimals.txt
Fox
Fox
Beaver
Rabbit
Beaver
Fox

### Purpose
The purpose of using the uniq command is to determine what the repeated lines are in a file. The purpose of using the wc -l command is to show the number of lines in a file. You can adda semicolon between the two commands to run both of them

uniq ; wc -l wildanimals.txt
Fox
Beaver
Rabbit
Beaver
Fox
6 wildanimals.txt

The output will show that the two successive fox lines that were repeated now only show one fox line, as well as it shows that there were 6 lines in the origional command.

### Purpose
