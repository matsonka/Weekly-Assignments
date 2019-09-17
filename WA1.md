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
The purpose of using the uniq command is to determine what the repeated lines are in a file. The purpose of using the wc -l command is to show the number of lines in a file. You can add a semicolon between the two commands to run both of them.

uniq ; wc -l wildanimals.txt
Fox
Beaver
Rabbit
Beaver
Fox
6 wildanimals.txt

The output will show that the two successive fox lines that were repeated now only show one fox line, as well as it shows that there were 6 lines in the origional command.



# Commands for looking into the file for Halloween
First a file would have to have been created before called halloween.txt that has to do with Halloween.

### Purpose
The purpose of using the cat command is to view a single file. The purpose of using the grep command is to look for a string of characters in a certain file.

$cat ; grep ghost halloween.txt

Once the command is run the output would then show the given file name of halloween.txt for the cat command and then it will show any words that contain the string of characters of ghost that was entered. So the output will read the following:

halloween.txt
ghost
ghost adventures
ghost hunters


# Commands for 


