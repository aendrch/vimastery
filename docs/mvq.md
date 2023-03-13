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

```
Vim "navigation" is not-so difficult!
```

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

* _Shift-Right-arrow_ | Go to the right, word by word
* _Shift-Left-arrow_ | Go to the left, word by word

> _Related tip_: While in Insert mode, you can press **Ctrl-o** to get back to Normal mode and execute command, after which you'll be automatically returned to Insert mode.

### Basic search

Vim has many search related options.

_All search operations ins Normal mode_

You can search forward by pressing ```/``` and then typing search pattern. Pressing _Esc_ will cancel it, while pressing _Enter_ will perform the search. Once you hit _Enter_, you can press ```n``` to search forward for the next occurence, or ```N``` to search backwards.

Now, let's try to figure out what would be the command to find the first match:

1. First march, is usually placed "on the top" of all others.
2. We already mentioned that command to jump to the top of a file is ```gg```.
3. And now we know that pressing ```n``` while searching will take us to next search pattern occurrence.

So, if you perform a search for a pattern, and you want to jump to the first match, you need to hit ```ggn```. Yup, this way we tell Vim: "go to the top of the file and find next (actually first occurrence)".

It's the same logic for the command to take you to the last match of your search. As you might already guess. it's ```GN```.

You can search backwards by pressing ```?``` and then typing your search pattern. Pressing ```n``` searches in the same direction (in this case backwards), while ```N``` searches in the opposite direction (in this case forwards).

### Searching for the current word

Vim can search for words under your cursor. In Normal mode, place your cursor to any word.

Press ```*``` and Vim will search forwards for the next occurrence of that word! How cool is that!

Press ```#``` and Vim will search backwards for the word under yourcursor.

These two commands are searching for exact words. So if you perform the search using these commands while your cursor is on word ```master```, it would not find the word ```mastering```.

So if you don't want exact word matching, use commands ```g*``` and ```g#``` accordingly.

### Search history

Vim keeps a search history. Just type ```/``` or ```?``` and use the arrow up down keys to go through previous search commands. Of course, you can edit a command (or only a pattern) you find in history and press _Enter_ to search again.

Let's say the cursor is on a word, and you want to search for a similar word. Instead of typing the entire word, here's what you can do:

1. Press ```/```
2. Then press ```Ctrl-r``` and then ```Ctrl-w```.

This will copy the current word under cursor to the command line, ready for searching. Now you can edit it and press _Enter_.

Once you're done with searching, you can hit _Ctrl-o to jump back to your previous position (or _Ctrl-i_ which will jump forwards).

What if you search for the last searched pattern again? There's no need to type the pattern again, or ever fo through history. Just press ```/``` and hit _Enter_ - an empty search pattern will repeat the last search. This will also work for ```:s``` and ```:g``` commands, which we'll cover later.

Vim also allows you to enter a count before search. For example, what if you want to jump to the fifht occurrence of the pattern? Simply type ```5/pattern```. Also, typing ```6*``` will search for the sixt occurrence of the current word under the cursor.

We have just covered the most important search basics.

## File Manager (netwr) in Vim

Vim comes with a built-in **netwr** plugin which is a great way to browse file and directories within a Vim session. This file manager supports four ways of displaying files and directories.

You can launch netwr in several ways like:

* ```:Ex``` - open current directory in current Vim window (remember it as a shortcut of **Ex**plore).
* ```:Ex <dir>``` - open specified directory ```<dir>```.
* ```:Sex``` - open current directory in horizontal split window (fun fact: Vim is the only editor in the world which has Sex as a command!).
* ```:Vex``` - open current directory in vertical split window.
* ```:Tex``` - open current directory in a new tab.
* ```:Lexplore``` - open current directory in vertical split on the left. Default setting opens files in the window to the right of thenetrw window.

Try out these commands and see which one works the best for you. I prefer to have a file explorer in a vertical split. I usually run:

```
:40vs +Ex
```

to open current directory in vertical split window with width of 40 columns.

After you read the chapter on mapping, you'll know how to create a shortcut for this command, so you can open and close file explorer quickly.

You can change the directory listing view to show more or less information, change the sorting order or hide some kinds of files. Once you start netwr, try to hit ```i``` to cycle through the view types. There are four of them: thin, long, wide and tree. Once you choose your favorite, set it to be the default one in your ```.vimrc``` file, like:

```
let g:netrw_liststyle = 3
```

### Changing how files are opened

With Vim, not only can you open files, but you can also open directories! Yes, go ahead and try to open some directory. For example this command:

```
$ vim /home/kidfella
``` 

will open my home directory. What I'll get is a list of all files and list of all subdirectories in the directory I've opened.

When you open a directory with Vim, you actually started netrw. So yes, that’s the way to start it out of Vim. Now, it’s important to know that you can perform some of the basic file manager operations using netrw:

* ```<Enter>``` - opens the file under the cursor, or enters the directory under the cursor
* ```D``` - deletes the file under the cursor. You can visually select multiple files and use this command to delete all of them.
* ```R``` - renames the file under the cursor.
* ```X``` - executes the file under the cursor.
* ```%``` - creates a new file in the current directory. Vim will ask you for a file name and open a buffer.

By default, when you hit Enter to open a file, it will be opened in the same window as the netrw. That’s not really practical. You would usually like to keep netrw in a side split, and load your files in another split. Fortunately, this behavior can be changed with netrw_browse_split option. To make the selection permanent add the following to your ```.vimrc```:

```
let g:netrw_browse_split = 4
```

Option ```4``` is the one I personally prefer. It open files in previous window (the current split you have beside netrw split).

## Set netrw split width
How file explorer will position a window for the new file you open, can be set with the netrw_browse_split option. If you’d like to setthe width of netrw split to 20% of your entire Vim window, put this in your ```.vimrc```:

```
let g:netrw_winsize = 20
```

