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

## 02/10/17

1. Build a commutator  
The commutator is used to power the motor coils. We had no issues with construction at this time.

2. Add a support shaft  
The inserted nails support the motor and allow it to rotate. We had no issues with construction at this time. 

3. Wind the armature coil  
The coil cuts the magnetic field which causes motion when a current is flowing. We had a small amount trouble whilst winding (tangling etc.), but nothing too major. We ended up with 120 turns in our coil.

4. Build the shaft support and magnet brackets  
5. Build the baseplate  
These components are use to hold the commutator and coil whilst it spins. We had some issues when attaching the supports to the baseplate, but we managed to solve this problem by using extra washers.

## 09/10/17

1. Finish the motor
2. Test the motor
Initially we had some issues as we hadn't correctly turned on the power supply, once this was corrected the motor turned successfully. From our tests we found a few issues with the design that we should be able to fix with future iterations. These issues are as follows:  
* Crumpled commutator - Through the building process the commutator became damaged, this caused some issues whilst the motor was in motion.  
* Single wire brushes - We used stripped single core wire as the motor brushes, and used our hands to support them. These two factors caused a very unreliable connection.  
* Loose motor supports - The paper clip motor supports allowed for quite a lot a shifting when the motor was turning.  

3. A better DC motor
We began the design for our next DC motor at the end of the session, we will use what we learnt from our previous attempt to ensure a more reliable system. 
