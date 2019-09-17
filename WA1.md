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


# Commands for Grocery Shopping List
First a file would have to have been created before called groceryshoppinglist.txt, which is comprised of a list of groceries that need to be bought

groceryshoppinglist.txt  
Cereal  
Milk  
Honey  
Bread  
Eggs


### Purpose
The purpose of using the sed command is to insert, replace (substitute), or delete parts of a file. Here the sed command's purpose is to replace a part of the file. The purpose of the find command is to find files or directories, and here the find command will be used to find a a certain file.


So we want to find our grocery shopping list in our files so we need to first use the find command.
$find groceryshoppinglist.txt

Now we can use the sed command to replace the parts of the shopping list that we already bought with something else that we need to buy

$sed 's/Milk/Syrup/' groceryshoppinglist.txt  
Cereal  
Syrup  
Honey  
Bread  
Eggs
