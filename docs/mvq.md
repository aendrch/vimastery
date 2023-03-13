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

### Set netrw split width
How file explorer will position a window for the new file you open, can be set with the netrw_browse_split option. If you’d like to setthe width of netrw split to 20% of your entire Vim window, put this in your ```.vimrc```:

```
let g:netrw_winsize = 20
```

## Editing files via SSH

One of the lesser known features of Vim is the ability to edit files remotely, over the network. This feature comes with the netrw plugin. To achieve this, netrw uses the SSH protocol, and manages remote files via the scp command.

Here’s how to do it:

```
vim scp://user@myserver[:port]//path/to/file.txt
```

Note the double ```/``` for the directory on the remote host, which is needed to correctly resolve the absolute path. ```[:port]``` is optional.

So with the command above you can open a file located on a remote host for editing.

What actually happens in the background is that Vim uses ```scp``` to download the requested file from a remote machine to a local ```/tmp``` directory, and then opens it for editing. When you save your changes to the file, the changes are first applied to a local copy in ```/tmp``` directory. After that, the file is uploaded via scp to the remote host.

If you open a directory on a remote host, you could also use netrw to browse through remote files and directories. The important thing is to always specify the directory path with ```/``` at the end.

Of course, it’s recommended that you use SSH keys for authentication. Otherwise, you might be asked for the SSH password too often.

Beside SSH, there are other protocols supported such as sftp, ftp, dav, etc.

For example, to open a file on a remote FTP server, you could run a command like:
```
vim ftp://hostname/path/to/file
```

Netrw offers lots of options and possibilities for remote editing, so for more information on this, take a look at ```:help scp```.

## Personalizing Vim

If you’ve had any experience with some of the text editors for programmers, it’s most likely you’ll be disappointed with how Vim looks.But this is actually a good thing. While other editors try to force you use their features, Vim does the opposite.

The “interface” is very minimal. This means that you have to spend some time and effort to make the Vim interface look pretty, as well as to improve your productivity. The benefit is this process of configuration will help you understand better how Vim works.

### Vim configuration explained

As a first step, we have to understand how to configure Vim. There are multiple configuration files, which can reside on different locations in your system, depending on which operating system you use or where have you installed Vim.

The main configuration file is vimrc. It exists in two versions—global and personal. Your personal vimrc file is usually placed in yourhome directory. In Linux operating systems it’s usually a hidden file called ```.vimrc```.

Whatever you change in this file will overrule any previous settings in the global vimrc file. If you’re not sure of your home directory location, run this command in Vim: ```:echo $HOME```.

The permanent configuration is set through ```.vimrc.``` But you can also configure the current Vim session. For example, if you’ve started Vim, and you don’t have line numbers shown, you can run the command:
```
:set number
```

to enable line numbers for the current session. If you’d like to disable this option for the current Vim session, you’d run:

```
:set nonumber
```

Another way to enable/disable boolean options is to use exclamation point ```!```. In this case, we could enable line numbers (assuming they're disabled) with a command:

```
:set number!
```

### Make Vim look beautiful

Vim allows its users to change the colors it uses. So yes, Vim supports color schemes. To begin, choose some of the installed color schemes. Later you can create your own, or download some you like, and install them in Vim.

In order to choose your color scheme, open a file with some source code. Then type: ```:colorscheme``` and press _Tab_. Then press Enter. You’ll see what the scheme looks like. Repeat the same command, just press Tab more times, until you find the color scheme you like. Once you find it, add to your ```.vimrc``` file:

```
colorscheme scheme_name
```

Sometimes, in a big file with lots of code and syntax coloring, it can be difficult to track your cursor. That’s why it’s a good tip to mark the line the cursor is currently in. You can try this out by typing ```:set cursorline``` in Vim, or to make this permanent, add to your ```.vimrc``` file:

```
set cursorline
```

If you don’t like the styling of the line, you can change it like this, for example: 

```
:highlight CursorLine guibg=lightblue ctermbg=lightgrey
```

If you really have a problem in following your cursor, then you can use a command to mark the current column of the cursor, coloring the entire column: ```set cursorcolumn```. 

Of course, it’s really important to add the line numbers, so also put: ```set nu[mber]``` to your ```.vimrc``` file.

If you want to enable spell checking for default, English language, you should add this: ```set spell```. If you want spell checking enabled for some other language, you can do it this way (example for German language): ```set spelllang=de```. If you want spell checking for more languages at once, no problem: ```set spelllang=en``` ,```de```,```it```. Of course, if you change spelllang setting to a language that’s not installed, Vim will ask you if it should try to download it.

You can always check the configuration of any Vim setting by adding a ````?``` to the end of its name.

For example:

```
set spell?
nospell
```

### Usability improvements

Default Vim settings are not really great. If you’re going to use Vim seriously, then it’s definitely worth it to spend some time on configuration. As we already said, all the configuration we’ll manage through the ```.vimrc``` file.

In this part, I will give you a list of different Vim settings, which you should consider and try out. At the end of this chapter, you’ll also find a snippet of basic recommended options, which you can just copy to your .vimrc file. Later on, you can continue with configuration on your own.

### General configuration options:

* ```set nocompatible``` - Use Vim settings, rather then Vi settings. It’s important to have this on the top of your file, as it influences other options.
* ```set backspace=indent,eol,start``` - Allow backspacing over indention, line breaks and insertion start.
* ```set history=1000``` - Set bigger history of executed commands.
* ```set showcmd``` - Show incomplete commands at the bottom.
* ```set showmode``` - Show current mode at the bottom.
* ```set autoread``` - Automatically re-read files if unmodified inside Vim.
* ```set hidden``` - Manage multiple buffers effectively: the current buffer can be “sent” to the background without writing to disk. When a background buffer becomes current again, marks and undo-history are remembered. See chapter Buffers to understand this better.

### User Interface Options

* ```set laststatus=2``` - Always display the status bar.
* ```set ruler``` - Always show cursor position.
* ```set wildmenu``` - Display command line’s tab complete options as a menu.
* ```set tabpagemax=40``` - Maximum number of tab pages that can be opened from the command line.
* ``` colorscheme desert``` - Change color scheme.
* ```set cursorline``` - Highlight the line currently under cursor.
* ```set number``` - Show line numbers on the sidebar.
* ```set relativenumber``` - Show line number on the current line and relative numbers on all other lines. Works only if the option above (number) is enabled.
* ```set noerrorbells``` - Disable beep on errors.
* ```set visualbell``` - Flash the screen instead of beeping on errors.

* ```set mouse=a``` - Enable mouse for scrolling and resizing.
* ```set background=dark``` - Use colors that suit a dark background.
* ```set title``` - Set the window’s title, reflecting the file currently being edited.

### Swap and backup file options - disable all of them:

* ```set noswapfile```
* ```set nobackup```
* ```set nowb```

### Indentation options:

* ```set autoindent``` - New lines inherit the indentation of previous lines.
* ```filetype plugin indent on``` - Smart auto indentation (instead of old smartindent option).
* ```set tabstop=4``` - Show existing tab with 4 spaces width.
* ```set shiftwidth=2``` - When indenting with ‘>’, use 2 spaces width.
* ```set expandtab``` - On pressing tab, insert 4 spaces.
* ```set nowrap``` - Don’t wrap lines.

### Search options:

* ```set incsearch``` - Find the next match as we type the search.
* ```set hlsearch``` - Highlight searches by default.
* ```set ignorecase``` - Ignore case when searching . . .
* ```set smartcase``` - . . . unless you type a capital.

### Text rendering options

* ```set encoding=utf-8``` - Use an encoding that supports Unicode.
* ```set linebreak``` - Wrap lines at convenient points, avoid wrapping a line in the middle of a word.
* ```set scrolloff=3``` - The number of screen lines to keep above and below the cursor.
* ```set sidescrolloff=5``` - The number of screen columns to keep to the left and right of the cursor.
* ```syntax enable``` - Enable syntax highlighting.

### Miscellaneous Options

* ```set confirm``` - Display a confirmation dialog when closing an unsaved file.
* ```set nomodeline``` - Ignore file’s mode lines; use vimrc configurations instead.
* ```set nrformats-=octal``` - Interpret octal as decimal when incrementing numbers.
* ```set shell``` - The shell used to execute commands.
* ```set spell``` - Enable spellchecking.

### Status line
The statusline in Vim is the bar along the bottom of the Vim window. The purpose of statusline is to give you various information about the status of the current buffer. The default statusline includes info like file path, permissions, line numbers and a percentage number of where you are in the file.

Although the default statusline offers quite a nice set of information, you can always improve it, if desired. There are even a couple of quite popular plugins for this purpose.

We’re going to cover just the basics, so if you want to modify your status line, you know how to.

Status line, by default, is shown only if you have more than one buffer open. However, it’s better to show it all the time, and you can do this by setting:

```
"show status line
set laststatus=2
```

in your ```.vimrc file.``` You’ll also notice a line ```"show status line```, which is a comment describing this option. So whenever you want to add a comment in ```.vimrc``` file, start the line with ```"``` character.

If, for some reason, you want to disable it, this is what you need:

```
set laststatus=0
```

Status line can be set like this in your ```.vimrc``` file:

```
set statusline=%F%m%r%h%w%=(%{&ff}/%Y)\ (line\ %l\/%L,\ col\ %c)
```

This can be a bit hard to read and understand if you’re a beginner. A different way of setting it
could be something like:

```
set statusline=%t	 "tail of the filename
set statusline+=%{&ff}	 "file format
set statusline+=%h	 "help file flag
set statusline+=%m	 "modified flag
set statusline+=%r	 "read only flag
set statusline+=%y	 "filetype
set statusline+=%c,	 "cursor column
set statusline+=%l/%L	 "cursor line/total lines
set statusline+=\ %P	 "percent through file
```

This format is much more useful, especially if you’d like to experiment with your status line. The easiest way to configure your status line is with the built in flags.

For example,```%m``` shows a ```[+]``` if the current buffer is modified. Using %L shows the total number of lines of the current file.

Of course, there are many of them, and that’s out of the scope for this book. Take a look at ```:help``` statusline for more information on them.

> Related tip: Using command __g Ctrl-g__, you can show the detailed information about the number of lines, words, characters, etc. in your current buffer

### Backup files

Vim can make backups of files you edit, so you’re safe from losing data. I don’t use this Vim feature personally, and I would suggest you set up a better backup solution for your work.

Of course, this feature can be useful. Backups are controlled by the settings of two options: ```backup``` and ```writebackup```. If interested, look these up in ```:help```.

Just like for swap files, you can also keep backup files better organized, by creating a directory and adding it to your ```.vimrc```:

```
set backupdir=~/.vim/.backup//
```

### Project specific .vimrc

If you’re working on multiple different projects, with different types of files, you might want to have specific configurations for some types of your projects.

Vim allows you to have a project specific ```.vimrc``` file. First you need to enable it by adding this to
your ```.vimrc```:

```
" enable project speficific vimrc
set exrc
```

Then you need to create your specific project ```.vimrc``` file configuration in the root of your project folder. This way, you can keep your main ```.vimrc``` file nice and clean, and have a specific configuration for other projects.

### Basic recommended configuration

It will take you some time and experience to configure Vim to fit your needs. You can copy this snippet to your ```.vimrc``` file to get you started. I recommend you start with this minimal (but good!) configuration.

As you progress through the book, your configuration will improve. Most importantly, once you start using Vim regularly, you’ll get ideas on what you’d like to improve and change. At that time, come back to this chapter and enable additional options you might need. Also, Google is your friend. Over time, you’ll be able to pick up tricks and configuration options from other advanced Vim users.

But take your time, and don’t spend a lot of time tweaking your Vim configuration right now. Use this configuration from below, and keep learning.

Here’s the basic configuration which you can use right away:

```
set nocompatible 	" Use Vim settings, rather than Vi settings
set softtabstop=2 	" Indent by 2 spaces when hitting tab
set shiftwidth=4 	" Indent by 4 spaces when auto-indenting
set tabstop=4 	" Show existing tab with 4 spaces width
syntax on 	" Enable syntax highlighting
filetype indent on 	" Enable indenting for files
set autoindent 	" Enable auto indenting
set number 	" Enable line numbers
colorscheme desert 	" Set nice looking colorscheme
set nobackup 	" Disable backup files
set laststatus=2 	"show status line
set statusline=%F%m%r%h%w%=(%{&ff}/%Y)\ (line\ %l\/%L,\ col\ %c)\
set wildmenu 	" Display command line's tab complete options as a menu.
```

