---
title: "Getting Started with Cobra"
date: 2019-03-03T17:10:59-05:00
draft: "true"
categories:
- programming
- golang
- howto
tags:
- golang
keywords:
- programming
- golang
#thumbnailImagePosition: left
#thumbnailImage: //example.com/image.jpg
---

[Golang](https://golang.org/) is a great language for systems programming, it compiles really fast, concurrency model is well designed, and creates statically compiled executables. That last one, the creation of statically compiled executables makes systems engineers lives very easy. No more copying dependencies from dev ⇒ test ⇒ prod.

While golang helps developers create programs that are easily deployed and distributed, it did not really help developers create the modern CLI UIs that users expect.

That is where [Cobra](https://github.com/spf13/cobra) steps in. Cobra gives developers an easy way to create complex UIs implementing fully POSIX-compliant flags.

I thought the best way to describe cobra is by building an example application. If you want to skip straight to the source you can find the repository [here](https://github.com/tracyde/cobra-example).

Lets get started. Here is what we are going to try and create:

```bash
cobra-example command arg --flag

# Welcome to cobra-example
# you executed the command: command
# and passed in the arg: arg
# flags: flag were passed
```

First we have to install the cobra library

```bash
go get -u github.com/spf13/cobra/cobra
```

## create rootCmd

## create second command

## Create variable to hold flag value

## Assign flags to command

<!--more-->
