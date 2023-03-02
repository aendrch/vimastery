# Notes
> _Don't wish Vim was easier, wish you were better!_

## Mastering Vim - Basics

WSL2 - Ubuntu 22.04

My Vim version: 8.2

Ubuntu command to install (with clipboard support): ```apt install vim-gtk3```

Some useful commands:

* ```:wq <filename>``` - Command to **save the file and exit Vim**. Letter ```w``` comes from write and letter ```q``` comes from quit
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

### Commands

Commands are probably the most important concept in Vim. Most of what you’ll do within Vim
will be the result of executing different kinds of commands. In general, we can say that there
are three ways of executing commands in Vim:

**Ex commands**

This is any command you can run as ```:{command}```, for example ```:help```. You will use them often.
You can see the entire list of these commands (it’s very long, don’t do it now) by running
```:help ex-cmd-index```.

**Mapped commands**

Any (more complex) commands, which we map or bind to some keys for easier access, belong
to this group. You’ll usually add these commands to your ```.vimrc``` file.

**Editing commands**

These are the commands which you’ll usually use in Normal and Insert mode. These are
commands like ```d4w``` which will delete four words after your cursor.

## Working with files

### Opening files

Here are the two most common methods for opening files in Vim.

**Method 1** - Open file from terminal

Once you open your terminal, type ```vim``` and then the filename. Example:

```
$ vim /etc/passwd
```

**Method 2** - Open file from Vim

When you start Vim by running ```vim``` in your terminal. there will be no files loaded, by default. Then, run command: ```:e <filename>``` to open a file in your existing Vim session.

Example:
```
$ vim
:e /etc/passwd
```

Very often you’d like to get the content of some other file into your current opened file. Actually,
to be more precise, instead of “current opened file,” from now on, we’ll use the term “current
buffer.”
So when you open an existing file, the content of this file is loaded in one Vim buffer. You’ll learn
much more about buffers later, but for now, just remember that buffer is a piece of memory
that’s been loaded with the content of a file.

Of course, you could open the second file, copy the content you need, return to first file, and
paste. But, there’s a better way.

Vim has a **r**ead command:

```
:read
:r
```

You can use this command to insert a file, or the output from a system command, into the
current buffer.
Here are a few examples of how you can use it:

* ```:r file.txt``` - Insert the file file.txt below the cursor in the current buffer.
* ```:0r file.txt ``` - Insert the file file.txt before the first line.
* ```:r!sed -n 2,8p file.txt``` - Insert lines 2 to 8 from file file.txt below the cursor.
* ```:r !ls``` - Insert a directory listing below the cursor.

All of these should be run in Normal mode. The last command will work only in Linux
or macOS.

> _Related tip_: Using command gf, you can open a file whose name (or path) is under or after
the cursor. Remember it as "goto file". Similarly, using gx command, you can open links in
your default browser.

### Closing files 

There are more than a few ways to close a file in Vim. Here are some of the most common ways.

* ```:wq``` - Save currently opened file and exit Vim (even if file is not changed).
* ```:x``` - Exit Vim but write only when changes have been made.
* ```ZZ``` - Equivalent to ```:x```. Notice there's no ```:```. This is a key press.
* ```:q!``` - Exit Vim without saving currently opened file.
* ```:qa``` - Exit all open files in current Vim session.
