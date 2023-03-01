# Notes
_Don't wish Vim was easier, wish you were better!_

## Mastering Vim - Basics

WSL2 - Ubuntu 22.04

My Vim version: 8.2

Ubuntu command to install (with clipboard support): ```apt install vim-gtk3```

Some useful commands:

* ```:wq <filename>``` - Command to **save the file and exit Vim**. Letter ```w``` comes from write and letter ```q``` comes from quit.* ```:q!``` - Command to close the file without saving it. 
* ```+NUM ``` - The cursor will be positioned on the line “NUM” for the first file you open.
* ```+/{pattern} ``` -  The cursor will be positioned on the first line containing “pattern” in the first
file you open.
* ```+cmd``` or ```-c cmd ``` -  Command “cmd” will be executed after the first file has been read. It’s interpreted as an Ex command. You’ll learn about Ex commands soon.
* ```-x ``` -  Use encryption to read or write files. You need to use this option only the first time
for a given file. Every following time you’ll be asked for the password even without this
option. The encryption implementation is not strong, so don’t rely only on this protection
for your important data.

## Vim Concepts

### Modes

Vim has twelve modes in total. 4 or 5 for the daily use.

The most important ones:

**Normal mode** - When you start Vim, by default you’ll be in Normal mode. In this mode you can
enter all the normal editor commands. It’s mostly used for navigation and text manipulation.
Advanced Vim users spend most of their time in Normal mode. A good habit to adopt and keep
in mind: whenever you’re not typing, it’s better to get back to Normal mode.

**Insert mode** - As the name says, this is for inserting new text. In this mode you can also run
some of the commands. By default, “– INSERT –” is shown at the bottom of Vim window.

**Command mode** - In this mode you can run Ex commands (like ```:set number```), enter search
patterns (like /```word```) and enter filter commands. After running the command, Vim returns to
Normal mode.

**Visual mode** - For navigation and manipulation of text selections. It’s similar to Normal
mode, but the movement commands extend a highlighted area. When you use a non-movement
command, it’s executed for the highlighted area. By default, there is “– VISUAL –” shown at the
bottom of the window.

**Insert Normal mode** - When you’re in Insert mode, and press _Ctrl-o_, you’ll enter this mode.
It’s similar to Vim Normal mode, but after executing one command, Vim returns to Insert mode.
By default, ‘– (insert) –’ is shown at the bottom of the window

