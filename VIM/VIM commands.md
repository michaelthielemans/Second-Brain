Modes:
------
i or a -> insert mode
o -> insert mode start on next line
v -> visual mode / mark text mode

commands:

x -> delete char
u -> undo
p -> paste
y -> yank line
dd -> delete line
d + arrowkey -> delete char that is selected
x -> delete selected char
w -> jump to next word
b -> jump to previous word
e -> jump to next words last char
:q -> quit
:wq -> quit with saving
:q! -> quit withou saving
:e <filename> -> open a second file in a new buffer
:bn -> buffer next
:bv -> buffer previous
:split <filename> open a second file the same window
:splitv <filename> vertical splitscreen

v visualmode
------------
y -> yank a selection
p -> past the selection

# Cursor movement

h - move cursor left
j - move cursor down
k - move cursor up
l - move cursor right
gj - move cursor down (multi-line text)
gk - move cursor up (multi-line text)
H - move to top of screen
M - move to middle of screen
L - move to bottom of screen
w - jump forwards to the start of a word
W - jump forwards to the start of a word (words can contain punctuation)
e - jump forwards to the end of a word
E - jump forwards to the end of a word (words can contain punctuation)
b - jump backwards to the start of a word
B - jump backwards to the start of a word (words can contain punctuation)
ge - jump backwards to the end of a word
gE - jump backwards to the end of a word (words can contain punctuation)
% - move cursor to matching character (default supported pairs: '()', '{}', '[]' - use `:h matchpairs`in vim for more info)
0 - jump to the start of the line
^ - jump to the first non-blank character of the line
$ - jump to the end of the line
g_ - jump to the last non-blank character of the line
gg - go to the first line of the document
G - go to the last line of the document
5gg or 5G - go to line 5
gd - move to local declaration
gD - move to global declaration
fx - jump to next occurrence of character x
tx - jump to before next occurrence of character x
Fx - jump to the previous occurrence of character x
Tx - jump to after previous occurrence of character x
; - repeat previous f, t, F or T movement
, - repeat previous f, t, F or T movement, backwards
} - jump to next paragraph (or function/block, when editing code)
{ - jump to previous paragraph (or function/block, when editing code)
zz - center cursor on screen
zt - position cursor on top of the screen
zb - position cursor on bottom of the screen
Ctrl + e - move screen down one line (without moving cursor)
Ctrl + y - move screen up one line (without moving cursor)
Ctrl + b - move screen up one page (cursor to last line)
Ctrl + f - move screen down one page (cursor to first line)
Ctrl + d - move cursor and screen down 1/2 page
Ctrl + u - move cursor and screen up 1/2 page

**Tip** Prefix a cursor movement command with a number to repeat it. For example, 4jmoves down 4 lines.


## Working with multiple files

:e[dit] file - edit a file in a new buffer
:bn[ext] - go to the next buffer
:bp[revious] - go to the previous buffer
:bd[elete] - delete a buffer (close a file)
:b[uffer]# - go to a buffer by index #
:b[uffer] file - go to a buffer by file
:ls or :buffers - list all open buffers
:sp[lit] file - open a file in a new buffer and split window
:vs[plit] file - open a file in a new buffer and vertically split window
:vert[ical] ba[ll] - edit all buffers as vertical windows
:tab ba[ll] - edit all buffers as tabs