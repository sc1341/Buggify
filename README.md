# Buggify Overview
Buggify is a Python bugger which automatically inserts a random variety of syntax and logical errors into a program file. 

Assuming we select testfile.py to be buggified, two files will be automatically generated:
- testfileBUGGIFIED.py -> _The version of the file with all the bugs added to it._
- testfileBUG-ANSWERKEY.py.txt -> _The answer key which contains a Diff between the two files showing what has changed._

Buggify is a great tool for educational/training purposes, interview/coding challenges, or even as a way to prank your friends!

# How To Run This
## Create a windows Executable File (.EXE)
~~~~~~
>pip3 install pyinstaller
>pyinstaller Buggify.py --onefile
~~~~~~

## Command Line Usage

>> python3 Buggify.py -h

usage: Buggify.py [-h] [--numberofbugs NUMBEROFBUGS]
                  [--bugs [{ps,zs,ees,addsubs,sbs,abs,abs2,abs3,ls,chars,cases,eqs,ifs,csc,ts,numc,mb,scl,buggedc,buggeddoc,all} [{ps,zs,ees,addsubs,sbs,abs,abs2,abs3,ls,chars,cases,eqs,ifs,csc,ts,numc,mb,scl,buggedc,buggeddoc,all} ...]]]
                  [--scriptpath SCRIPTPATH] [--GUI GUI]

Buggify! Check the README.md for more information!

optional arguments:
  -h, --help            show this help message and exit
  --numberofbugs NUMBEROFBUGS
                        The number of bugs you want put in the script
  --bugs [{ps,zs,ees,addsubs,sbs,abs,abs2,abs3,ls,chars,cases,eqs,ifs,csc,ts,numc,mb,scl,buggedc,buggeddoc,all} [{ps,zs,ees,addsubs,sbs,abs,abs2,abs3,ls,chars,cases,eqs,ifs,csc,ts,numc,mb,scl,buggedc,buggeddoc,all} ...]]
                        The specified bugs, see key in the README
  --scriptpath SCRIPTPATH
                        Absolute path of the script to be 'Buggified'
  --GUI GUI             Launch GUI Interface (usage: --GUI yes



## The default values are:
number of bugs = 20
filepath = A pop up window will appear from the cmd
bugs = a random selection of bugs

## Command Line Abbriviations

Below are the abbriviated versions of each bug by name, these can be specified by the user

'ps' == period_switch
'zs' == zero_o_switch
'ees' == elif_else_switch
'addsubs' == add_subtract_switch
'sbs' == single_bracket_switch
'abs' == all_bracket_switch1
'abs2' == all_bracket_switch2
'abs3' == all_bracket_switch3
'ls' == line_switch
'chars' == char_switch
'cases' == case_switch
'eqs' == equal_switch
'ifs' == if_switch
'csc' == camel_snake_case
'ts' == tabs_spaces
'numc' == num_change
'mb' == missing_blanks
'scl' == scrambled_line
'buggedc' == bugged_comment
'buggeddoc' == bugged_docstring
'all' == all bugs
                 

## Buggify.buggify()

You can also import Buggify and run it with Python. This allows some additional options. 
~~~~
>>>from Buggify import Buggify
>>>b = Buggify()
>>>b.buggify('testfile.py', 15) #Type the full path to the file if it's not in the same directory.
~~~~
Run Buggify 20 times on the same file to generate 20 unique Buggified copies:
~~~~
>>>from Buggify import Buggify
>>>b = Buggify()
>>>for x in range(20):
>>>    b.buggify('testfile.py', 15')
~~~~
Run Buggify on every file in the current directory with the default 20 bugs:
~~~~
>>>import os
>>>from Buggify import Buggify
>>>files = [file for file in os.listdir('.') if os.path.isfile(file)] #Creates a list of all the files in the current directory
>>>b = Buggify()
>>>for file in files:
>>>    b.buggify(file)
~~~~
Run Buggify on every file in the current directory and all of its subdirectories with the default 20 bugs:
~~~~
>>>import os
>>>from Buggify import Buggify
>>>list_of_files = []
>>>for root, subfolders, files in os.walk("."):
>>>    for file in files:
>>>        path = os.path.join(root, file)
>>>        filepath = os.path.abspath(path)
>>>        list_of_files.append(filepath)
>>>
>>>b = Buggify()
>>>
>>>for file in list_of_files:
>>>    b.buggify(file)
~~~~
___
# Buggify.py Overview
The Class that does all the work is Buggify:
~~~~
from Buggify import Buggify
b = Buggify()
b.buggify(num_bugs, file)
~~~~
 1. Specify the number of bugs you'd like to introduce and the file you'd like to apply the bugs to. If the number of bugs is left blank, it will default to 20. If the file isn't specified, the user will be prompted to choose one.  
 2. The file is copied to a new file with "BUGGIFIED" appended to the file name but before the extension. This ensures that no changes will be made to the original file.
 3. buggify() calls on **bug_function_list** which is a global list that stores all the different bug functions. Num_bugs acts as a range in a foor loop and each time buggify() chooses one function at random from this list to insert into the new copied file.
 4. Once completed, a diff is stored as a new text file showing the differences between the original and Buggified files. The diff is renamed with "BUG-ANSWERKEY" appended to the file name.

# Classes

## Buggify
The Buggify class is our main class that creates instances of the CreateBugs and FileManager classes that control the main parts of the code. Buggify is created in the 'if __name__ == "__main__"' after the arguments are parsed. The Buggify Class also takes 1 argument which is the bug_function_list, this list is the list of abbriviated bugs to include when the program is run through.

## FileManager
The File Manager Class holds all of the functions that have to do with copying, altering or changing files. 

## CreateBugs:
The Create Bugs Class holds the functions that create the bugs in the loaded file, these functions are isolated from everything else to make the code easier to read. These CreateBug functions have shortened version that are typed in by the user through the command line. The full list of these abbriviations are availible above in the README.md


## Implemented Bug functions in bug_function_list

*(These Functions are held inside the CreateBugs class, if the user specifies spacific functions to be run in the GUI or command line, then a custom list is created that excludes the unwanted functions. If the 'all' option on the GUI or no values are specified, then all of the functions have the possiblity to be run on the script being modified by Buggify)*

 - **period_switch()**
	 - Switches a period to a comma and vice versa.
	 ~~~~
	 - line_char_list.insert(char_index + 1, '=')
	 ~~~~ 
	 ~~~~
	 + line_char_list,insert(char_index + 1. '=')
	 ~~~~ 
	 
 - **zero_o_switch()**
	 - Switches a zero to a lower case 'o' and vice versa.
	 ~~~~
	 - random_index = random.randint(0, len(line_char_list) - 1)
         + random_index = rand0m.randint(o, len(line_char_list) - 1)
	 ~~~~
	 
 - **elif_else_switch()**
	 - Switches "else" to "elif" and vice versa.
	 ~~~~
	  if randomizer == 0:
              line_char_list.insert(0, ' ')
         - elif randomizer == 1:
              del line_char_list[0]
         - else randomizer == 2:
	 ~~~~
	 ~~~~
	  if randomizer == 0:
              line_char_list.insert(0, ' ')
         + else randomizer == 1:
              del line_char_list[0]
         + elif randomizer == 2:
	 ~~~~
	 
 - **add_subtract_switch()**
	 - Switches a '+' to a '-' and vice versa.
	 ~~~~
	 - line_char_list[char_index - 1] not in ['=','!','+','-'] and
	 ~~~~ 
	 ~~~~
	 + line_char_list[char_index + 1] not in ['=','!','-','+'] and
	 ~~~~ 
	 
 - **single_bracket_switch()**
	- A bracket character is changed with another bracket type character once per line.
	 ~~~~
	 - if filelist[line_index][hash_index - 1].isspace() and random.randint(1, 3) == 1:
         + if filelist{line_index)[hash_index - 1).isspace(] and random.randint{1, 3] == 1;
	 ~~~~
	 
 - **all_bracket_switch1()**
 	- All parentheses found in a line are switched with square brackets and vice versa.
	~~~~
	- if filelist[line_index][hash_index - 1].isspace() and random.randint(1, 3) == 1:
	+ if filelist(line_index)(hash_index - 1).isspace[] and random.randint[1, 3] == 1:
	~~~~
	~~~~
	- random_index = random.randint(0, len(line_char_list) - 1)
	+ random_index = random.randint[0, len[line_char_list] - 1]
	~~~~
	
 - **all_bracket_switch2()**
 	- All parentheses found in a line are switched with curly brackes and vice versa.
	~~~~
	- if filelist[line_index][hash_index - 1].isspace() and random.randint(1, 3) == 1:
	+ if filelist[line_index][hash_index - 1].isspace{} and random.randint{1, 3} == 1:
	~~~~
	~~~~
	- random_index = random.randint(0, len(line_char_list) - 1)
	+ random_index = random.randint{0, len{line_char_list} - 1}
	~~~~
	
 - **all_bracket_switch3()**
 	- All square backets found in a line are switched with curly braces and vice versa.
	~~~~
	- if filelist[line_index][hash_index - 1].isspace() and random.randint(1, 3) == 1:
	+ if filelist{line_index}{hash_index - 1}.isspace() and random.randint(1, 3) == 1:
	~~~~
	~~~~
	- [num for num in doc_list if doc_list.index(num) % 2 == 0]
	+ {num for num in doc_list if doc_list.index(num) % 2 == 0}
	~~~~
	
 - **line_switch()**
	 - Switches a full line with the line before it.
	 ~~~~
	  line_char_list[x] = line_char_list[x].replace(char1, char2)
         - num_bugs -=1
         - break
	 ~~~~
	 ~~~~
	 line_char_list[x] = line_char_list[x].replace(char1, char2)
         + break
         + num_bugs -=1
	 ~~~~
	 
 - **char_switch()**
 	- Switches a character with the one before it.
	~~~~	    
    - return new_filelist, num_bugs_update
	~~~~	
	~~~~	    
    + return new_filelsit, num_bugs_update
    	~~~~

 - **case_switch()**
	 - Switches the first character in a word from lower case to upper case and vice versa.
	 ~~~~
	 - random_line_index = Random_line(filelist, 'no_line_list')
	 ~~~~
	 ~~~~
	 - Random_line_index = random_line(filelist, 'no_line_list')
	 ~~~~

 - **equal_switch()**
	 - Switches a double equals sign '==' to a single equals sign '=' and vice versa.
	 ~~~~
	 - start_quotes = [x for x in doc_list if doc_list.index(x) % 2 == 0]
	 ~~~~
	 ~~~~
	 + start_quotes == [x for x in doc_list if doc_list.index(x) % 2 = 0]
	 ~~~~

 - **if_switch()**
	 - Option #1:
		 - Removes the 'if' from the beginning of a line and the ':' from the end of a line.
		 ~~~~
		-  if line_char_list[char_index] == 0:
                	line_char_list[char_index] += 1
		 ~~~~
		 ~~~~
		 +  line_char_list[char_index] == 0
                    line_char_list[char_index] += 1
		 ~~~~
	    - Option #2: 
		    - Adds an 'if' to the beginning of the line and a ':' to the end of the line. 
		      Additionally, the following line is indented with four additional spaces.
		    ~~~~
		    - first_line = filelist[random_line_index]
		    - second_line = filelist[random_line_index - 1]
		    ~~~~
		    ~~~~
		    + if first_line = filelist[random_line_index]:
		    +     second_line = filelist[random_line_index - 1]
		    ~~~~

 - **camel_snake_case()**
	 - Switches a phrase written in snake_case to camelCase and vice versa.
	 ~~~~
	 - line_char_list = filelist[lineIndex].split(' ')
	 ~~~~
	 ~~~~
	 + lineCharList = filelist[line_index].split(' ')
	 ~~~~
	 
 - **tabs_spaces()**
	 - Option #1:
		 - Four spaces in the beginning of a line are increased by 1.
		 ~~~~
		 -    line_list = list(filelist[random_line_index])
		 +     line_list = list(filelist[random_line_index])
		 ~~~~
	 - Option #2:
		 - Four spaces in the beginning of a line are decreased by 1.
		 ~~~~
		 -    line_list = list(filelist[random_line_index])
		 +   line_list = list(filelist[random_line_index])
		 ~~~~ 
	 - Option #3:
		 - Four spaces in the beginning of a line are increased by 4 (a double tab).
		 ~~~~
		 -    line_list = list(filelist[random_line_index])
		 +        line_list = list(filelist[random_line_index])
		 ~~~~
	 - Option #4:
		 - A line which originally didn't have any spaces in the beginning has four spaces inserted at its beginning.
		 ~~~~
		 - def zero_o_switch(filelist, num_bugs):
		 +     def zero_o_switch(filelist, num_bugs):
		 ~~~~
		 
- **num_change()**
	 - An integer is either increased or decreased by 1.
	 ~~~~
	 - line_char_list[x] = line_char_list[x].replace(char2, char1)
	 ~~~~ 
	 ~~~~
	 + line_char_list[x] = line_char_list[x].replace(char1, char2)
	 ~~~~ 

- **missing_blanks()**
	 - One third of all non-white space characters in a random line	are replaced with underscores .
	   Appends "#Fill in the missing blanks!".
	 ~~~~
	 - while line_char_list.count('_') > 5:
	 ~~~~ 
	 ~~~~
	 + _hile _i_e__ha__list._ou_t_'_'_ > 5: #Fill in the missing blanks!
	 ~~~~ 
	 
- **scrambled_line()**
	 - Randomly rearranges all the words (defined as separated by whitespace) in a random line.
	   Appends "#Scrambled line!".
	 ~~~~
	 - for y in range(start_quotes[x], end_quotes[x] + 1):
	 ~~~~ 
	 ~~~~
	 + in y 1): for range(start_quotes[x], end_quotes[x] + #Scrambled line!
	 ~~~~

 - **bugged_comment()** 
	 - A comment beginning with a "#" is replaced with *#BUGGIFIED COMMENT*. 
	 While not a syntax or logical error *per se*, it does make the code more difficult to understand.  
	  ~~~~ 
            if full_file_path == '':
          - #Removes small Tk window and prompts user to choose file.
            Tk().withdraw()
	  ~~~~
	  ~~~~
	    if full_file_path == '':
          + #BUGGIFIED COMMENT
            Tk().withdraw()
	  ~~~~
	 
 - **bugged_docstring()**
	 - A full docstring is replaced with *#BUGGIFIED DOCSTRING*. 
	   This is similar to bugged_comment() in that its not a syntax or logical error *per se*, 
	   but it does make functions more difficult to understand.
	 ~~~~
	  def tabs_spaces(filelist, num_bugs):
         -    '''
         -    Randomly adds or subtracts a space in a tabbed line,
         -    or adds a tab or double tab where it doesn't belong.
         -    '''
	 ~~~~
	 ~~~~
	  def tabs_spaces(filelist, num_bugs):
         +    #BUGGIFIED DOCSTRING
         +    #BUGGIFIED DOCSTRING
         +    #BUGGIFIED DOCSTRING
         +    #BUGGIFIED DOCSTRING
	 ~~~~
