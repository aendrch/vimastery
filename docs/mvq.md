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

### Saving files

There are several ways to save a file in Vim. When you save the file, you actually write the contents of the buffer to the disk. That's why, the command for saving is "**w**rite".

Here are the most common commands you should know:

* ```:w``` - Save currently opened file (which was previously saved).
* ```:w file.txt``` - Save currently opened file as ```file.txt```.
* ```:w! file.txt``` - Save file as ```file.txt``` with overwrite option.
* ```:sav file.txt``` - Save current buffer as a new ```file.txt```.
* ```:up[date] file.txt``` - Like ```:w``` but only save when the buffer has been modified.

### Navigation 

In order to be truly efficient with Vim, you have to learn how to properly navigate through your files, buffers, help system, etc. This section will enable you to improve your navigation speed drastically.

**Basic movement**

Just like in any other text editor, you can use arrow keys (Up, Down, Left, Right) to move around within your text Vim. But, in Vim, there's an alternative.

Most advanced Vim users prefer to keep their hands fingers around the home row on akeyboard. This is possible, because instead of arrows, you can use _keys h, j, k_ and _l_ for navigation. 

* _h_ - left
* _j_ - down
* _k_ - up
* _l_ - right

In the beginning, it might be hard to get used to these. The first problem is to remember which key does what. Here’s my suggestion for how to remember them:

Look at your keyboard and notice how _j_ looks like an arrow down, with a half head. So _j_ takes your cursor one position down. These keys are positioned in this way(assuming you’re using aqwerty keyboard layout): _H J K L_.

The key far **right** is _l_ and it will take you to the **right**. The key far **left** is _h_ and it will take you to the **left**. Two keys remain in the middle, _j_ and _k_.

### Navigate through words

It will take you some time to get used to, but I highly recommend that you try to adopt this kind of navigation. When youb operate on a single line (or even a few), instead of movin one character up, down, left or right, you can move between words. Also, ther are some other useful shortcuts you should remember.

* ```w``` - Go to the start of the next **w**ord.
* ```W``` - Go to the start of the next **W**ord.
* ```e``` - Go to the **e**nd of the current **word**.
* ```E``` - Go to the previous (**b**efore) **word**.
* ```b``` - Go to the previous (**b**efore) **word**.
* ```B``` - Go to the previous (**b**efore) **WORD**.

```WORD``` consist of a sequence of a non-blank characters. It's always delimited by white space. On the other hand, ```word``` is delimited by non-keyword characters, whic are configurable. Remember that ```word``` ends at a non-word character, such as a ., - or ) .

For example, in sentence:

```Vim "navigation" is not-so difficult!```

we have 5 ```WORDS```: ```Vim "navigation" is not-so difficult!```, all delimited by white space. However, we have 10 ```words```.

So if you're navigating through source code, and want to stop at delimiters and characters like ( ) . { } , $ use  ```w```. If you're working with text and want to skip these, then use ```W```. For more information, take a look at ```:help 03.1```.

### Scrolling pages

Note: All of these commands for navigation can take a number as a prefix. For example ```3w``` will take you to the start of the 3rd next word, while ```6j``` will take your file page by page, you can use the following shortcuts:

* ```Ctrl-d``` - Scroll **d**own half page
* ```Ctrl-u``` - Scroll **u**p half page
* ```Ctrl-f``` - Scroll down **f**ull page (or **f**orwards)
* ```Ctrl-b``` - Scroll up full page (to **b**eginning, or **b**ackwards)

### Jumping around the file

Vim offers you simple ways to go to the beginning or end of your file. This can be very handy when you’re working with large files. Beside these, in the table below, there are a few more handy shortcuts for jumping through the file:

* ```gg``` - Go to the top of the file
* ```G``` - Go to the bottom of the file
* ```{``` - Go to the beginning of the current paragraph
* ```}``` - Go to the end of the current paragraph
* ```%``` - Go to the matching pair of ( ), [ ], { }
* ```50%``` - Go to the line at the 50% of the file
* ```:NUM``` - Go to line NUM. ```:28``` jumps to line 28

### Navigating inside the window

Here are a few handy shortcuts you can benefit from, when it comes to moving your cursor in the current Vim window:

* ```H``` - Move cursor to first (**h**ighest) line in current window.
* ```L``` - Move cursor to **l**owest line in current window.
* ```M``` - Move cursor to the (**m**iddle line in current window.

### Navigating in Insert mode

If you want to move around and make edits in Insert mode, you shouldn't, most of the time. The proper way would be to hit _Esc_ to getNormal mode, go to the correct location, make an edit, and get back to Insert mode.

For example, you could press _Ctrl-o_ ```F m``` to move to previous ```m``` character and get Insert mode.

However, sometimes, you'd find it easier to stay in Insert mode. In these cases, using arrow keys to move arround is usually not fast enough. Here's what you could do:

* _Shift-Right-arrow | Go to the right, word by word
* _Shift-Left-arrow  | Go to the left, word by word

_Related tip_: While in Insert mode, you can press **Ctrl-o** to get back to Normal mode and execute command, after which you'll be automatically returned to Insert mode.


