commands:

modes: 
```
esc               -command mode   
i                 -insert mode  
set number        -line numbers
:q                -quit
:wq               -write and quit
:q!               -quit without saving
dd                -delete a line
[number]dd        -delete specified number of lines from cursor
ctrl+r            -redo
u                 -undo

Navigation
_______________________________________
H                       –go to the first line of current screen.
M                       –go to the middle line of current screen.
L                       –go to the last line of current screen.
ctrl+f                  –jump forward one full screen.
ctrl+b                  –jump backwards one full screen.
ctrl+d                  –jump forward (down) a half screen.
ctrl+u                  –jump back (up) one half screen.

Seach 
________________________
/[word]                 -search the word in the text
n                       -go down to the next matching word
N                       -go up to previous matching word
%s/[word]/[replace]/gc  -find word and replace, to replace all occurance '/g' for all the word '/gc' ask for confirmation to replace words



copy
cscope
ctag
```
