+++
categories = ["shell", "bash", "howto"]
date = "2008-03-26T21:54:02-04:00"
description = "How to get colored output from ls"
draft = "false"
keywords = ["bash", "shell"]
title = "Colored ls Output"

+++

Unix uses the `ls` command to list the contents of a directory. By default `ls` displays all directories and files the same way, leaving you without the ability to quickly determine what type of files you are looking at (in Unix everything is a file). Here is an screenshot showing the default output of `ls` on OS X:

{{< figure src="/tutorial/images/terminal_ls_default.png" alt="Default OS X ls output" >}}

`ls` has the ability to color code different file types by passing the `--color` option to `ls`. For example, type the following command at your shell prompt to see colorized output:

```bash
ls --color
```

Here is what that command looks like:

{{< figure src="/tutorial/images/terminal_ls_tweaked.png" alt="OS X tweaked ls output" >}}

If you get an error statement after running the last command then you most likely do not have the GNU version of `ls` installed. You can download the GNU version of `ls` by downloading and installing the [GNU Coreutils](http://www.gnu.org/software/coreutils/) package for your OS.

If you are not using xterm as your terminal you may have to set the `TERM` environment variable to `xterm` or `xterm-color`. The `TERM` setting you choose will depend on your OS and distribution. You change your `TERM` variable by running the following:

```bash
export TERM=xterm-color
```

or

```bash
export TERM=xterm
```

To make your `TERM` environment variable persistent you add either of the commands above to your `$HOME/.bash_profile` or `$HOME/.bashrc` just like we did for the alias definition.

To customize the color `ls` displays you must modify the `LS_COLORS` environment variable. `LS_COLORS` is formatted as a string of variables separated by colons. Changing `LS_COLORS` is out of the scope of this howto.

## Creating an Alias

Typing `ls --color` everytime you need to use `ls` seems a little tedious, that is where the wonderful `alias` command comes in. `alias` allows you to create a shorthand definition to replace a command or a series of commands. To create an alias you can either put your alias definition in the `$HOME/.bash_profile` or `$HOME/.bashrc` which is persistent across multiple logins and shells or you can specify an alias definition at the command line. Examples of both are below:

Adding an alias definition to `$HOME/.bash_profile`

```bash
echo "alias ls='ls --color'" >> $HOME/.bash_profile
```

If you want to put the alias definition in `$HOME/.bashrc` just substitute it instead of `$HOME/.bash_profile` in the example above.

Create an alias definition that will only be valid for your current shell session perform the following:

```bash
alias ls='ls --color'
```

Now whenever you use `ls` it will use colored output.