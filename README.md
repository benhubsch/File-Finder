# File-Finder

A command-line program that removes the hassle of finding and opening files and directories.

## Table of Contents

- [Project Overview](#project Overview)
- [Installation](#installation)
- [Usage](#usage)
- [Support](#support)
- [Contributing](#contributing)

## Project Overview

SOME WORDS

## Installation

Installation is most easily done using the setup.py file that can be found in this repository. However, installation does depend on the [Click library](https://github.com/pallets/click) for user configuration options (common file paths, favorite text editor, etc.). If you haven't already installed it, then go ahead and install that before proceeding with the following commands on the command line:

```
$ python3 setup.py
```

## Usage

The structure of most all commands will be roughly as follows:

```
$ ff [file or directory name] [-flag]
```
Note that every command works with both files and directories. If you issue a command that feels unnatural, such as changing directories to a file called helloWorld.js, the program will intelligently change to the directory in which helloWorld.js is contained since changing directories to helloWorld.js makes no sense.

There are 4 main flags you can use: --change-directory (aliased as -c), --open-editor (-e), --open-finder (-f), and --duplicated (-d).
Changing directories is fairly straightforward and can be done as follows:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/c.png "Changing Directories")
You'll notice that there's a folder on my Desktop called Find Me, which the program is able to find with ease, despite the fact that it's in a different directory from the one I'm currently in. It's also worth noting that my directory name had a space in it but was still found!

Opening a file or directory in your favorite editor has similar syntax, but with a flag -e:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/editor.png "Opening an editor")
During setup, I specified Atom as my text editor, so the directory opened in Atom automatically. And it contains a file called found.java! Cool!

Next, I can open any file or directory in a new window in the Mac Finder application using the flag -f:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/finder.png "Opening Mac Finder")
Again, we see the familiar found.java contained within the folder Find Me.

Lastly, you can add the duplicated flag to any command if you think there's a chance that you might have two files or directories of the same name in your file system. If you only have one, it will assume that it's the one you want and will perform the relevant action like it would without the duplicated flag. If you have multiple, you will be given the opportunity to specify the file that you would like the action to be performed on.

Here is an example where I have a file called found.java that exists in multiple places, but I want to change my current working directory to one of them. I can use the -d flag in combination with the -c flag to deal with that:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/duplicate.png "Duplicates cd")
The program now finds every instance of found.java, records their absolute file paths, and ulimately gives me the option to pick one of them. I enter the number 1, so my directory is changed to "Sophomore Duke", which corresponds to my choice.

Those are the basics!

You can also always type
```
$ ff --help
```
to remind yourself of the available commands if you ever forget.

## Support

Please note that this is application is currently only funcitonal on OS X. [Open an issue](https://github.com/benhubsch/File-Finder/issues/new) for support.

## Contributing

I would love any and all help with this project! I still need to make this compatible on other operating systems, and I think it'd be cool to clean up the setup process and make it installable using pip. Create a branch, add commits, and [open a pull request](https://github.com/benhubsch/File-Finder/compare/).
