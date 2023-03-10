# Welcome to my rich CMDOW cli

The CMDOW cli is a command line interface for the CMDOW tool. It is written in python and is a work in progress.

## The CMDOW cli

The goal is to make a command line interface for CMDOW that is easy to use and has a rich feature set.
To avoid python's (and [pandas'](https://pandas.pydata.org/) overhead, [the cli uses polars](https://github.com/pola-rs/polars) to do the heavy lifting.

## The CMDOW tool

CMDOW is a command line tool for Windows that allows you to control windows. It is written in C++ and is available on [the author's webpage.](https://ritchielawrence.github.io/cmdow/)

### Why use CMDOW?

I just stumbled upon CMDOW and I think it is a great tool. It is very powerful and allows you to do a lot of smart stuff with regards to windows. As a humble side project, I decided to write a command line interface for CMDOW that is easy to use and has a rich feature set.

For example, CMDOW allows you to do the following:

Get a list of all windows and their positions/sizes (in pixels):

```powershell
cmdow /p /f
```

However the output was pure text, and I wanted to add a little bit of spark to it. So I wrote a python script that uses [polars](https://github.com/pola-rs/polars) to parse the output and make it a bit more readable. You can get the same output as above by running the following command:

```powershell
rcmdow raw
```

Note that the `raw` command is just an alias for `cmdow /p /f`.
To add a little bit of spark to the output, you can run the following command:

```powershell
rcmdow ls
```

This will give you a nice table with the windows and their positions/sizes.

## Features / Usage

### Get information about windows

The equivalent of `cmdow /t /p /f` (which lists only taskbar windows) can be achieved by running the following command:

```powershell
rcmdow lst
```

To let the cli tool guess what your current layout is, run the following command:

```powershell
rcmdow layout
```

This output is just a filter on top of the `rcmdow ls` command. It will show you all windows that are visible on your screen.

### Move windows

So far the cli tool only supports screen splitting. You can split your screen into two halves by running the following command:

Left/Right:

```powershell
rcmdow hzl name1 name2
```

You can get the names of the windows by running the `rcmdow ls` or `rcmdow lst` command and selecting the `Image` column.
Note that the names are **not case sensitive.**

Top/Bottom:

```powershell
rcmdow vtl name1 name2
```

## Installation

### Prerequisites

- Python 3.8 or higher
- The CMDOW tool (available [here](https://ritchielawrence.github.io/cmdow/))

### An easy way to install

I recommend using [scoop](https://scoop.sh/) to install the CMDOW cli. It is a command line installer for Windows that makes installing and updating software a breeze.

To install scoop, run the following command in powershell:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time
irm get.scoop.sh | iex
```

To install the CMDOW cli, run the following command in powershell:

```powershell
scoop bucket add extras
scoop install cmdow
```

**Note:** The cli tool assumes you can call cmdow from the command line. If you installed CMDOW to a different location, you will have to add the location to your PATH variable.