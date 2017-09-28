# Roco222 Lab Book
## 25/09/17

1. Write your first markdown document  
Here are the the basic syntax rules of markdown:  
# Hash is used to denote a heading, with additional hashes being used for further sub-headings    
**Bold is represented using either double asterisk or underscore either side of what you want bold**  
_Italics is represented using either an asterisk or an underscore either side of what you want to have in italic_  

Paragraphs are separated by a blank line

Two spaces at the end of a line leaves a line break  
Three dashes create a horizontal rule:  
--- 
* Asterisks are used to create a bullet list  
1. Numbers and periods create a number list  
[Putting text in square brackets creates a link, with the url of the link in brackets afterwords](http://example.com)  
 
2. Command-Line 101  
* ls - list directory contents
* cd /tmp - changes directory to a tempory directory
* cd $HOME - changes directory to the home directory, the $ represents the user account 
* mkdir - used to make directories
* echo "Hello" > hello.md - outputs the text "Hello" and saves it to a .md file
* cat hello.md - outputs the text in the .md file
* cp hello.md hello-again.md - copies the contents of hello.md into a new file
* mv hello-again.md hello-hello.md - renames file
* rm hello.md - removes the file 
* rm -rf - force deletes everything (doesn't work in practice)
* cat /proc/cpuinfo - displays the specs of the cpu

4. Your first git repository  
ls -al - displays all data on the files and folders in the selected directory, it shows things such  
as the number of bits and the creation date and time of each file and folder.

6. Version tracking 
So far i've learnt that git uses repositories to store data. These repositories allow tracking of the  
various versions of added data through the use of commit messages. Repositories can be stored locally  
or online.
