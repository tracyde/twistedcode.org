+++
categories = ["shell", "bash", "howto"]
date = "2007-11-18T22:27:04-05:00"
description = "How to customize your bash prompt"
draft = "false"
keywords = ["bash", "shell"]
title = "Customizing your bash prompt"

+++

I came to OS X from the wonderful world of Linux; upon doing so I really missed my customized terminal prompt; after all, the default Mac OS X prompt is really boring and blah.

{{< figure src="/tutorial/images/terminal_default.png" alt="Default OS X Terminal" >}}

Customizing the default shell prompt not only makes the terminal that much more exciting, it will also help you remember which system you are currently on and the directory you are about to run a command in (Yea!, no more incessant `pwd` commands).  This is especially useful for those late night pesky phone calls letting you know that you have to come into work early, really, really early; to fix the server that the underpaid incompetent third string sysadmin was supposed to be watching!  Arriving on site with multiple windows open mixed with sleep deprivation can have some very devastating results.  Running shutdown or init in the wrong window can really hurt.

## Bash Prompt Variables

The primary Bash shell prompt is customized by setting the $PS1 shell environment variable.  In order to see what your current prompt is set to you must `echo $PS1`:

```bash
echo $PS1
```

Characters prefixed by a backslash (`\`) are actually variables that get expanded.  Here is a list of all Bash prompt variables as described in the PROMPTING section of the BASH(1) man page.

Variable Name  | Description
-------------  | -------------
`\a`           | an ASCII bell character (07)
`\d`           | the date in "Weekday Month Date" format (e.g., "Tue May 26")
`\D{format}`   | the format is passed to strftime(3) and the result is inserted into the prompt string; an empty format results in a locale-specific time representation. The braces are required.
`\e`           | an ASCII escape character (033)
`\h`           | the hostname up to the first `.`
`\H`           | the full hostname
`\j`           | the number of jobs currently managed by the shell
`\l`           | the basename of the shells terminal device name
`\n`           | newline
`\r`           | carriage return
`\s`           | the name of the shell, the basename of $0 (the portion following the final slash)
`\t`           | the current time in 24-hour HH:MM:SS format
`\T`           | the current time in 12-hour HH:MM:SS format
`\@`           | the current time in 12-hour am/pm format
`\A`           | the current time in 24-hour HH:MM format
`\u`           | the username of the current user
`\v`           | the version of bash (e.g., 2.00)
`\V`           | the release of bash, version + patch level (e.g., 2.00.0)
`\w`           | the current working directory, with $HOME abbreviated with a tilde
`\W`           | the basename of the current working directory, with $HOME abbreviated with a tilde
`\!`           | the history number of this command
`\#`           | the command number of this command
`\$`           | if the effective UID is 0, a `#`, otherwise a `$`
`\nnn`         | the character corresponding to the octal number `nnn`
`\\`           | a backslash
`\[`           | begin a sequence of non-printing characters, which could be used to embed a terminal control sequence into the prompt
`\]`           | end a sequence of non-printing characters

## Setting Your Prompt

Set your new prompt by manipulating the $PS1 variable.

```bash
export PS1='\h:\W \u\$ '
```

That would make your prompt look like this:

```bash
hostname:~ username$
```

To keep your settings for the next Bash shell, place a line in your `$HOME/.bashrc` that looks like this:

```bash
PS1='\h:\W \u\$ '
```

### *Mac users note the following*

Due to the way OS X and the Terminal application handle command emulation you have to create the file `$HOME/.bash_profile` and enter the following line:
```bash
source ~/.bashrc
```

Once you have done this every Terminal window you open up will have your custom prompt.

## Other Variables

`$PS1` is not the only shell variable that affects your prompt.  `$PS2` is the secondary prompt.  The secondary prompt shows up in command line loops:

```bash
hostname:~ username$ export PS2="--> "
hostname:~ username$ for x in $(seq 3); do
--> echo $x
--> done
1 2 3
hostname:~ username$
```

`$PS3` and `$PS4` also exist.  From the Bash Reference Manual:

Variable Name  | Description
-------------  | ------------
`PS1`          | the primary prompt string.  The default value is `'\s-\v\$ '`.
`PS2`          | the secondary prompt string.  The default value is `'> '`.
`PS3`          | the value of this variable is used as the prompt for the select command. If this variable is not set, the select command prompts with `'#? '`.
`PS4`          | the value is the prompt printed before the command line is echoed when the `-x` option is set (see The Set Builtin).  The first character of `PS4` is replicated multiple times, as necessary, to indicate multiple levels of indirection.  The default is `'+ '`.
`PROMPT_COMMAND`  | if set, the value is interpreted as a command to execute before the printing of each primary prompt (`$PS1`).  `$PROMPT_COMMAND` can be used in clever ways to run a command before each primary prompt display.  See below for an example

```bash
hostname:~ username$ export PROMPT_COMMAND='echo -n "$(uptime | cut -d',' -f1) "'<br />
14:33:01 up 6 days hostname:~ username$
```

## Time to Colorize!

Some of you might want to present your shell prompt using color.  This is especially useful for privileged shells.  Lets make the root shell display using red:

```bash
hostname:~ username$ export PS1="\e[01;31m\h:\W \u\$ \e[00m"
```

This might look a little confusing so let's break it down.

Escape Code  | Description
-----------  | -----------
`\e[`        | is the Escape Character sequence (you can also use `\[\033[`)
`01;31m`     | Sets the color to light (`01`) red (`31`)
`\h:\W \u\$` | Prints `hostname:(current directory) username$ `
`\e[`        | Escape Character sequence
`00m`        | Clears all color (no color after this point)

In this example if your username is alex, your hostname is 'hades', and you are currently in your $HOME directory the resulting prompt will look like:

```bash
hades:~ alex$ 
```

## Bash Color Escape Codes

Use any of the following escape codes between `\e[` and `m` to colorize text in Bash:

Color        | Escape Code
-----------  | -----------
Black        | `0;30`
Dark Gray    | `1;30`
Blue         | `0;34`
Light Blue   | `1;34`
Green        | `0;32`
Light Green  | `1;32`
Cyan         | `0;36`
Light Cyan   | `1;36`
Red          | `0;31`
Light Red    | `1;31`
Purple       | `0;35`
Light Purple | `1;35`
Brown        | `0;33`
Yellow       | `1;33`
Light Gray   | `0;37`
White        | `1;37`

## My custom prompt...

Just in case you were wondering what I have set my prompt to here we go:

```bash
PS1='\[\033[01;32m\]\u\[\033[01;34m\]::\[\033[01;31m\]\h \[\033[00;34m\]{ \[\033[01;34m\]\w \[\033[00;34m\]}\[\033[01;32m\]-> \[\033[00m\]'
```

Which looks like this:

{{< figure src="/tutorial/images/terminal_tweaked.png" alt="My Custom Bash Terminal" >}}

The `PS1` string does not span multiple lines.  I decided to use `\[033[` instead of `\e[` to maximize compatibility between different terminals (I like to take my custom shell everywhere I go).  If you would like a breakdown of my prompt feel free to ask in the comments below.

## References

Bash Reference Manual - http://www.gnu.org/software/bash/manual/bashref.html
Bash Prompt Howto - http://tldp.org/HOWTO/Bash-Prompt-HOWTO/
