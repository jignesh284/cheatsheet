
modes
_____________________________
```
esc               -command mode   
i                 -insert mode  
v                 -visual mode(to select)
```
commands
______________________
```
:set number        -line numbers
:q                -quit
:wq               -write and quit
:q!               -quit without saving
```
General
_____________________________
```
dw                -delete a word
dd                -delete a line
[number]dd        -delete specified number of lines from cursor
ctrl+r            -redo
u                 -undo
y                 -copy
p                 -paste
r                 -replace
```

Navigation
_______________________________________
```
             ^
             k              Hint:  The h key is at the left and moves left.
       < h       l >               The l key is at the right and moves right.
             j                     The j key looks like a down arrow.
             v



ctrl+f                  –jump forward one full screen.
ctrl+b                  –jump backwards one full screen.
ctrl+d                  –jump forward (down) a half screen.
ctrl+u                  –jump back (up) one half screen.
```

Inline Navigation
_______________________________________
```

H                       –go to the first line of current screen.
M                       –go to the middle line of current screen.
L                       –go to the last line of current screen.
0                       –go to the starting of the current line.
^                       –go to the first non blank character of the line.
$                       –go to the end of the current line.
g_                      –go to the last non blank character of the line
gg                      -go to the first line of the documenet
```


Word Navigation
_______________________________________
```
w                       –Takes you to the start of the word.
[number]w               -Take you forward by n words
b                       -Takes you backwards to the start of last work

e                       -Takes you to the end of the work
[number]e               -Take you end of 'nth words' from current
```


Seach 
________________________
```
/[word]                 -search the word in the text
n                       -go down to the next matching word
N                       -go up to previous matching word
%s/[word]/[replace]/gc  -find word and replace, to replace all occurance '/g' for all the word '/gc' ask for confirmation to replace words
```
