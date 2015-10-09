# Mac OS X Tricks and Tips #

Mac OS is an interesting beast with a slightly contradictory set of characteristics: the GUI is designed to be easy and to hide the workings of the computer from the user, while the Terminal provides direct access to the guts of Darwin. This document provides information about taking control of your Mac to make your work easier and to break down the artificial barrier between the GUI and the shell.

## GUI Tips ##

### Getting to your hard drive in Finder ###

As a default, Mac OS hides your hard drive from you. Instead, the Finder shows you a view of your mass storage as if your user directory were the root.

#### To include your disk in the Devices list in Finder ####

1.  Open or switch to a Finder window.
2.  In the **Finder** menu, select **Preferences...**.
3.  Select the **Sidebar** tab in **Finder Preferences**.
4.  In the **DEVICES** group, select the **Hard disks** checkbox.

#### To set an icon for your disk on the desktop ####

1.  Open or switch to a Finder window.
2.  In the **Finder** menu, select **Preferences...**.
3.  Select the **General** tab in **Finder Preferences** (it should be 
    selected by default).
4.  Under **Show these items on the desktop**, select the **Hard 
    disks** checkbox.

### Making system and hidden files visible in Finder ###

By default, Finder hides all system and hidden files from you. To make them visible:

1.  Open **Terminal**
2.  Enter the following command:

    ```bash
    $ defaults write com.apple.finder AppleShowAllFiles 1
    ```
3.  Restart Finder by hold down the option key, click-holding the 
    Finder icon on the Dock, and selecting **Releaunch** from the 
    pop-up menu. (If this doesn't work, you can use `killall Finder` from the shell.)

## BASH Tips ##

### Common commands ###

| Command            | Description                      |
| ------------------ | -------------------------------- |
| `$ pwd`            | Present working directory. Prints the path of the directory that you're in. |
| `$ ls`             | Lists the contents of the present working directory. Without further arguments, presents just the names of the non-hidden files. |
| `$ ls -lah`        | Lists the contents of the directory, including  all files (even hidden), in a detailed list, with file sizes abbreviated with memory designations (MB, e.g.) instead of number of bytes. | 


#### To open your present working directory in Finder ####

```bash
$ open .
```

#### To open a text file in TextEdit ####

Sometimes you'll want to make a quick change to a text file. If you are comfortable with vi, you can just use:

```bash
$ open mytext.file
```

You can also use the default text editor (TextEdit) to edit a file from teh command line:

```bash
$ open -e mytext.file
```
#### To substitute the output of one bash command inside the command line of another ####

For example, to concatenate a bunch of files that are listed in a file:

```bash
$ cat `cat infile` > outfile
```

