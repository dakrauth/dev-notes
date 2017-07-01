VI
==


.. note::
    Before doing anything to a document, type the following command followed 
    by a carriage return: :set showmode

.. note::

    Counts - Nearly every command may be preceded by a number that specifies how many times it is to be performed. For example, 5dw will delete 5 words and 3fe will move the cursor forward to the 3rd occurence of the letter e. Even insertions may be repeated conveniently with this method, say to insert the same line 100 times.


Starting VI
-----------

=========================   =================================================================
vi *filename*               Edits *filename*
vi -r *filename*            Edits last save version of *filename* after a crash
vi + *n* *filename*         Edits *filename* and places curser at line *n*
vi + *filename*             Edits *filename* and places curser on last line
vi +/*string* *filename*    Edits *filename* and places curser on first occurance of *string*
vi *filename* *file2* ...   Edits *filename*, then edits *file2* ... After the save, use :n
=========================   =================================================================

Ending VI
---------

======================= ============================================================
ZZ or :wq or :x         Saves and exits VI
:w                      Saves current file but doesn't exit
:w!                     Saves current file overriding normal checks but doesn't exit
:w *file*               Saves current as *file* but doesn't exit
:w! *file*              Saves to *file* overriding normal checks but doesn't exit
:*n,m* w *file*         Saves lines *n* through *m* to *file*
:*n,m* w <<*file*       Saves lines *n* through *m* to the end of *file*
:q                      Quits VI and may prompt if you need to save
:q!                     Quits VI and without saving
:e!                     Edits file discarding any unsaved changes (starts over)
:we!                    Saves and continues to edit current file
======================= ============================================================

Status
------

======   ===================================================================================================
:.=      Shows current line number
:=       Shows number of lines in file
^-G      Shows filename, current line number, total lines in file, and % of file location
======   ===================================================================================================


Inserting Text
--------------

===============     ================================================================
i                   Insert before cursor
I                   Insert before line
a                   Append after cursor
A                   Append after line
o                   Open a new line after current line
O                   Open a new line before current line
r                   Replace one character
R                   Replace many characters
^-v *char*          While inserting, ignores special meaning of char (e.g., for inserting characters like ESC and ^) until ESC is used
:r *file*           Reads *file* and inserts it after current line
:*n*fr *file*       Reads *file* and inserts it after line *n*
^-i or ``TAB``      While inserting, inserts one shift width
===============     ================================================================


While in Insert Mode
--------------------

================     ===========================================================
^-h or Backspace     While inserting, deletes previous character
^-w                  While inserting, deletes previous word
^-x                  While inserting, deletes to start of inserted text
^-v                  Take the next character literally. (i.e. To insert a ^-H, type ^-v ^-h)
================     ===========================================================

Motion
------

============ =============================================================================================================================================
h            Move left                                                                                                                                    
j            Move down                                                                                                                                    
k            Move up                                                                                                                                      
l            Move right                                                                                                                                   
Arrow Keys   These do work, but they may be too slow on big files. Also may have unpredictable results when arrow keys are not mapped correctly in client.
w            Move to next word                                                                                                                            
W            Move to next blank delimited word                                                                                                            
b            Move to the beginning of the word                                                                                                            
B            Move to the beginning of blank delimted word                                                                                                 
^            Moves to the first non-blank character in the current line                                                                                   
\+ or ``CR`` Moves to the first character in the next line                                                                                                
\-           Moves to the first non-blank character in the previous line                                                                                  
e            Move to the end of the word                                                                                                                  
E            Move to the end of Blank delimited word                                                                                                      
(            Move a sentance back                                                                                                                         
)            Move a sentance forward                                                                                                                      
{            Move a paragraph back                                                                                                                        
}            Move a paragraph forward                                                                                                                     
0 or |       Move to the begining of the line                                                                                                             
*n*\|        Moves to the column *n* in the current line                                                                                                
$            Move to the end of the line                                                                                                                  
1G           Move to the first line of the file                                                                                                           
G            Move to the last line of the file                                                                                                            
*n*\G        Move to *n* line of the file                                                                                                             
:*n*         Move to *n* line of the file                                                                                                             
fc           Move forward to c                                                                                                                            
Fc           Move back to c                                                                                                                               
H            Move to top of screen                                                                                                                        
*n*\H        Moves to *n* line from the top of the screen                                                                                             
M            Move to middle of screen                                                                                                                     
L            Move to botton of screen                                                                                                                     
*n*\L        Moves to *n* line from the bottom of the screen                                                                                          
^-d          Move forward 1/2 screen                                                                                                                      
^-f          Move forward one full screen                                                                                                                 
^-u          Move backward 1/2 screen                                                                                                                     
^-b          Move backward one full screen                                                                                                                
^-e          Moves screen up one line                                                                                                                     
^-y          Moves screen down one line                                                                                                                   
^-u          Moves screen up 1/2 page                                                                                                                     
^-d          Moves screen down 1/2 page                                                                                                                   
^-b          Moves screen up one page                                                                                                                     
^-f          Moves screen down one page                                                                                                                   
^-I          Redraws screen                                                                                                                               
z ``CR``     Makes the current line the top line on the page                                                                                              
*n*\z ``CR`` Makes the line *n* the top line on the page                                                                                                
z.           Makes the current line the middle line on the page                                                                                           
*n*\z.       Makes the line *n* the middle line on the page                                                                                             
z-           Makes the current line the bottom line on the page                                                                                           
*n*\z-       Makes the line *n* the bottom line on the page                                                                                             
%            Move to associated ( ), { }, [ ]                                                                                                             
============ =============================================================================================================================================

Deleting Text
-------------

.. note::

    Almost all deletion commands are performed by typing d followed by a
    motion. For example, dw deletes a word. A few other deletes are:


=================  ==============================================================================================================================================================================
x                  Delete character to the right of cursor                                                                                                                                       
*n*\x              Deletes n characters starting with current; omitting n deletes current character only                                                                                         
X                  Delete character to the left of cursor                                                                                                                                        
*n*\X              Deletes previous n characters; omitting n deletes previous character only                                                                                                     
D                  Delete to the end of the line                                                                                                                                                 
d$                 Deletes from the cursor to the end of the line                                                                                                                                
dd or :d           Delete current line                                                                                                                                                           
*n*\dw             Deletes the next *n* words starting with current                                                                                                                            
*n*\fdb            Deletes the previous *n* words starting with current                                                                                                                        
*n*\fdd            Deletes *n* lines beginning with the current line                                                                                                                           
:*n,m*\dd           Deletes lines *n* through *m*                                                                                                                                             
"*n*\fp            Retrieves the last *n* delete (last 9 deletes are kept in a buffer)                                                                                                       
=================  ==============================================================================================================================================================================

Yanking Text
------------

.. note::

    Like deletion, almost all yank commands are performed by typing y
    followed by a motion. For example, y$ yanks to the end of the
    line.


================================  ===============================================================================================================================================================================
yy                                Yank the current line                                                                                                                                                          
:y                                Yank the current line                                                                                                                                                          
*n*\fyy or *n*\fY                 Places *n* lines in the buffer-copies                                                                                                                                        
"(a-z) *n* fyy or "(a-z) *n* fdd  Copies or cuts (deletes) *n* lines into a named buffer a through z; omitting n works on current line                                                                         
================================  ===============================================================================================================================================================================

Changing text
-------------

.. note::

    The change command is a deletion command that leaves the editor in
    insert mode. It is performed by typing c followed by a motion. For
    example cw changes a word. A few other change commands are:


==========================  ==========================================================================
C                           Change to the end of the line                                             
cc or S                     Change the whole line until ESC is pressed                                
xp                          Switches character at cursor with following character                     
stext                       Substitutes text for the current character until ESC is used              
cwtext                      Changes current word to text until ESC is used                            
Ctext                       Changes rest of the current line to text until ESC is used                
cMotion_cmd                 Changes to text from current position to Motion Command until ESC is used 
<< or >>                    Shifts the line left or right (respectively) by one shift width (a tab)   
*n*\<< or *n*\>>            Shifts *n* lines left or right (respectively) by one shift width (a tab)
==========================  ==========================================================================

Putting text
------------

==================  ============================================================================
p                   Put after the position or after the line                                    
P                   Put before the poition or before the line                                   
"(a-z)p or "(a-z)P  Pastes text from a named buffer a through z after or before the current line
==================  ============================================================================

Markers
-------

.. note::

    Named markers may be set on any line in a file. Any lower case letter
    may be a marker name. Markers may also be used as limits for
    ranges.

===  =================================================
mc   Set marker c on this line                        
\`c  Go to beginning of marker c line.                
'c   Go to first non-blank character of marker c line.
===  =================================================

Search for strings
------------------

=============================  ===============================================================================================================================================================
/ *string*                     Search forward for *string*                                                                                                                                    
? *string*                     Search back for *string*                                                                                                                                       
n                              Search for next instance of *string*                                                                                                                           
N                              Search for previous instance of *string*                                                                                                                       
%                              Searches to beginning of balancing ( ) [ ] or { }                                                                                                              
f *char*                       Searches forward in current line to *char*                                                                                                                     
F *char*                       Searches backward in current line to *char*                                                                                                                    
t *char*                       Searches forward in current line to character before char                                                                                                      
T *char*                       Searches backward in current line to character before char                                                                                                     
?str                           Finds in reverse for str                                                                                                                                       
:set ic                        Ignores case when searching                                                                                                                                    
:set noic                      Pays attention to case when searching                                                                                                                          
:*n,m* s/*str1*/*str2*/*opt*   Searches from *n* to *m* for *str1*; Replaces *str1* to *str2*; *opt*: g: global change, c: confirm (y to acknowledge, to suppress), p: print changed lines
&                              Repeats last :s command                                                                                                                                        
:g/*str*/*cmd*                 Runs *cmd* on all lines that contain *str*                                                                                                                     
:g/*str1*/s/*str2*/*str3*/     Finds the line containing *str1*, replaces *str2* with *str3*                                                                                                  
:v/*str*/*cmd*                 Executes *cmd* on all lines that do not match *str*                                                                                                            
,                              Repeats, in reverse direction, last / or ? search command                                                                                                      
=============================  ===============================================================================================================================================================

Replace
-------

.. note::

    The search and replace function is accomplished with the :s command.
    It is commonly used in combination with ranges or the :g command
    (below).


=============================  =====================================================
:s/*pattern*/*string*/*flags*  Replace *pattern* with *string* according to *flags*.
g                              Flag - Replace all occurences of pattern             
c                              Flag - Confirm replaces.                             
&                              Repeat last :s command                               
=============================  =====================================================

Regular Expressions
-------------------

=======  ===============================================================================
. (dot)  Any single character except newline                                            
\*       zero or more occurances of any character                                       
[...]    Any single character specified in the set                                      
[^...]   Any single character not specified in the set                                  
\\<      Matches beginning of word                                                      
\\>      Matches end of word                                                            
^        Anchor - beginning of the line                                                 
$        Anchor - end of line                                                           
\(...\)  Grouping - usually used to group conditions                                    
\\ *n*   Contents of *n* grouping                                                   
\\       Escapes the meaning of the next character (e.g., \\$ allows you to search for $)
\\ \\    Escapes the \\ character                                                        
=======  ===============================================================================

[...] - Set Examples
--------------------

==================  ============================================================================================================================
[A-Z]               The SET from Capital A to Capital Z                                                                                         
[a-z]               The SET from lowercase a to lowercase z                                                                                     
[0-9]               The SET from 0 to 9 (All numerals)                                                                                          
[./=+]              The SET containing . (dot), / (slash), =, and +                                                                             
[-A-F]              The SET from Capital A to Capital F and the dash (dashes must be specified first)                                           
[0-9 A-Z]           The SET containing all capital letters and digits and a space                                                               
[A-Z][a-zA-Z]       In the first position, the SET from Capital A to Capital Z. In the second character position, the SET containing all letters
[a-z]{*m*}          Look for *m* occurances of the SET from lowercase a to lowercase z                                                     
[a-z]{*m,n*}        Look for at least *m* occurances, but no more than *n* occurances of the SET from lowercase a to lowercase z            
==================  ============================================================================================================================

Regular Expression Examples
---------------------------

===========  ==============================================================================================================
/Hello/      Matches if the line contains the value Hello                                                                  
/^TEST$/     Matches if the line contains TEST by itself                                                                   
/^[a-zA-Z]/  Matches if the line starts with any letter                                                                    
/^[a-z].*/   Matches if the first character of the line is a-z and there is at least one more of any character following it
/2134$/      Matches if line ends with 2134                                                                                
/\(21|35\)/  Matches if the line contains 21 or 35                                                                         
/[0-9]*/     Matches if there are zero or more numbers in the line                                                         
/^[^#]/      Matches if the first character is not a # in the line                                                         
===========  ==============================================================================================================

Ranges
------

.. note::

    Ranges may precede most "colon" commands and cause them to be executed
    on a line or lines. For example :3,7d would delete lines 3-7.
    Ranges are commonly combined with the :s command to perform a
    replacement on several lines, as with :.,$s/pattern/string/g to
    make a replacement from the current line to the end of the file.


=============  ========================================
:*n*,*m*       Range - Lines *n*-*m*               
:.             Range - Current line                    
:$             Range - Last line                       
:'c            Range - Marker c                        
:%             Range - All lines in file               
:g/*pattern*/  Range - All lines that contain *pattern*
=============  ========================================

Shell Functions
---------------

=============  =============================================================================================================================
:! cmd         Executes shell command cmd; you can add these special characters to indicate:% name of current file# name of last file edited
!! cmd         Executes shell command cmd, places output in file starting at current line                                                   
:!!            Executes last shell command                                                                                                  
:r! cmd        Reads and inserts output from cmd                                                                                            
:f file        Renames current file to file                                                                                                 
:w !cmd        Sends currently edited file to cmd as standard input and execute cmd                                                         
:cd dir        Changes current working directory to dir                                                                                     
:sh            Starts a sub-shell (^-d returns to editor)                                                                                
:so file       Reads and executes commands in file (file is a shell script)                                                                 
!}sort         Sorts from current position to end of paragraph and replaces text with sorted text                                           
=============  =============================================================================================================================

Files
-----

===========  =======================================
:w *file*    Write to *file*                        
:r *file*    Read *file* in after line              
:n           Go to next file                        
:p           Go to previous file                    
:e *file*    Edit *file*                            
!!<program>  Replace line with output from <program>
===========  =======================================

VI Settings
-----------

.. note::

    Options given are default. To change them, enter type :set option to
    turn them on or :set no*optioni* to turn them off.To make them
    execute every time you open VI, create a file in your HOME
    directory called .exrc and type the options without the colon (:)
    preceding the option


====================  ===============================================================
:set ai               Turns on auto indentation                                      
:set all              Prints all options to the screen                               
:set ap               Prints line after d c J m :s t u commands                      
:set bf               Discards control characters from input                         
:set dir=tmp          Sets *tmp* to directory or buffer file                         
:set eb               Precedes error messages with a bell                            
:set ic               Ignores case when searching                                    
:set lisp             Modifies brackets for Lisp compatibility.                      
:set list             Shows tabs (^l) and end of line ($)                            
:set magic            Allows pattern matching with special characters                
:set mesg             Allows others to send messages                                 
:set no<option>       Turns off *option*                                             
:set nu               Shows line numbers                                             
:set opt              Speeds output; eliminates automatic RETURN                     
:set prompt           Prompts for command input with :                               
:set re               Simulates smart terminal on dumb terminal                      
:set report           Indicates largest size of changes reported on status line      
:set ro               Changes file type to "read only"                               
:set scroll=n         set n lines for ^-d and z                                   
:set sh=shell_path    set shell escape (default is /bin/sh) to *shell_path*          
:set showmode         Indicates input or replace mode at bottom                      
:set sw=n             Sets shift width to *n* characters                           
:set term             Prints terminal type                                           
:set terse            Shorten messages with terse                                    
:set timeout          Eliminates one-second time limit for macros                    
:set tl=n             Sets significance of tags beyond *n* characters (0 means all)
:set ts=n             Sets tab stops to *n* for text input                         
:set wa               Inhibits normal checks before write commands                   
:set warn             Warns "no write since last change"                             
:set window=n         Sets number of lines in a text window to *n*                 
:set wm=n             Sets automatic wraparound *n* spaces from right margin.      
:set tabstop=4        N/A                                                            
:set shiftwidth=4     N/A                                                            
:set smarttab         N/A                                                            
:set expandtab        N/A                                                            
:set softtabstop=4    N/A                                                            
====================  ===============================================================

Key Mapping
-----------

.. note::

    Map allows you to define strings of VI commands. If you create a file called ".exrc"
    in your home directory, any map or set command you place inside this file will
    be executed every time you run VI. To imbed control characters like ESC in the
    macro, you need to precede them with ^-v. If you need to include quotes ("),
    precede them with a \ (backslash). Unused keys in vi are: K V g q v * = and
    the function keys.



====================  ==============================================
:map *key* *cmd_seq*  Defines *key* to run *cmd_seq* when pressed   
:map                  Displays all created macros on status line    
:unmap key            Removes macro definition for key              
:ab *str* *string*    When *str* is input, replaces it with *string*
:ab                   Displays all abbreviations                    
:una *str*            Unabbreviates *str*                           
====================  ==============================================

Other
-----

======  ===================================================================================================================
~       Toggle upp and lower case                                                                                          
J       Join lines                                                                                                         
*n*\J   Joins the next *n* lines together; omitting n joins the beginning of the next line to the end of the current line
.       Repeat last text-changing command                                                                                  
u       Undo last change (Note: u in combination with . can allow multiple levels of undo in some versions)                
U       Undo all changes to line                                                                                           
;       Repeats last f F t or T search command                                                                             
======  ===================================================================================================================

