# Notes
_Don't wish Vim was easier, wish you were better!_

## Mastering Vim - Basics

WSL2 - Ubuntu 22.04

My Vim version: 8.2

Ubuntu command to install (with clipboard support): ```apt install vim-gtk3```

Some useful commands:

* ```+NUM ``` - The cursor will be positioned on the line “NUM” for the first file you open.
* ```+/{pattern} ``` -  The cursor will be positioned on the first line containing “pattern” in the first
file you open.
* ```+cmd``` or ```-c cmd ``` -  Command “cmd” will be executed after the first file has been read. It’s interpreted as an Ex command. You’ll learn about Ex commands soon.
* ```-x ``` -  Use encryption to read or write files. You need to use this option only the first time
for a given file. Every following time you’ll be asked for the password even without this
option. The encryption implementation is not strong, so don’t rely only on this protection
for your important data.
