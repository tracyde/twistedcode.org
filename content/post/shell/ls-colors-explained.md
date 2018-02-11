+++
categories = ["shell", "bash", "howto"]
date = "2008-04-13T21:39:59-04:00"
description = "Explanation of LS_COLORS and associated parameters"
draft = "false"
keywords = ["bash", "shell"]
title = "LS_COLORS Explained"

+++

In my previous [article](/post/shell/colored-ls-output/) I showed you how to make the `ls` command display colored output; now I am going to show you how to customize what colors get displayed. We are going to use the `LS_COLORS` environment variable to accomplish this task.

You can change your `LS_COLORS` environment variable by setting it in your `$HOME/.bash_profile` or `$HOME/.bashrc` file. The syntax for `LS_COLORS` is as follows:

```bash
LS_COLORS='di=1:fi=0:ln=31:pi=5:so=5:bd=5:cd=5:or=31:*.deb=90'
```

The parameters for `LS_COLORS` (`di`, `fi`, `ln`, `pi`, etc) refer to different file types:

Paramater Name   | File Type
---------------- | -------------
 di              | Directory
 fi              | File
 ln              | Symbolic Link
 pi              | Fifo file
 so              | Socket file
 bd              | Block (buffered) special file
 cd              | Character (unbuffered) special file
 or              | Symbolic Link pointing to a non-existent file (orphan)
 mi              | Non-existent file pointed to by a symbolic link (visible when you type ls -l)
 ex              | File which is executable (ie. has 'x' set in permissions).

The `*.deb=90` parameter in the example above tells `ls` to display any files ending with a `.deb` extension using the color specified, 90 or dark grey in this case. This can be applied to any types of files (eg. you could use `*.jpg=33` to make JPEG files appear orange). Any number of parameters can go into the `LS_COLORS` variable, as long as the parameters are separated by colons.

## Color Codes

Through trial and error I worked out the color codes for `LS_COLORS` to be:

Code   | Color
------ | -------
  0    | Default Colour
  1    | Bold
  4    | Underlined
  5    | Flashing Text
  7    | Reverse Field
 31    | Red
 32    | Green
 33    | Orange
 34    | Blue
 35    | Purple
 36    | Cyan
 37    | Grey
 40    | Black Background
 41    | Red Background
 42    | Green Background
 43    | Orange Background
 44    | Blue Background
 45    | Purple Background
 46    | Cyan Background
 47    | Grey Background
 90    | Dark Grey
 91    | Light Red
 92    | Light Green
 93    | Yellow
 94    | Light Blue
 95    | Light Purple
 96    | Turquoise
 100   | Dark Grey Background
 101   | Light Red Background
 102   | Light Green Background
 103   | Yellow Background
 104   | Light Blue Background
 105   | Light Purple Background
 106   | Turquoise Background

These codes can also be combined with one another:

```bash
di=5;34;43
```

Setting the `LS_COLORS` `di` parameter to the above example will make directories appear in flashing blue text with an orange background (just because flashing text is available doesn't mean you should use it!)

Customizing the colors that `ls` uses to display its output can make sifting through your filesystem a bit easier.
