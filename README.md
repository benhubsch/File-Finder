# Insta-Nav

A command-line program that automates finding and opening files and directories and removes the hassle of searching for them manually.

## Table of Contents

- [Project Overview](#project-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Support](#support)
- [Contributing](#contributing)

## Project Overview

This was a fun, quirky project that sprung up one day when I got frustrated trying to find files while developing. To me it seemed ridiculous that there was no better way to get to files (if you didn't know exactly where they were) than to alternate between typing "cd" and "ls" commands over and over and over. When I searched on Github and the internet for a package that could search for files and directories automatically, I couldn't find one. Thus, I decided to write one myself! 

I used the [Click library](https://github.com/pallets/click) in Python, the ability to import OS to control a user's operating system activity, and os.path to help with joining the navigated paths together.

I'd never written a command-line application before, so the first thing I did was Google around for some nice resources I could use as a starting point. I ended up reading Click's entire documentation top to bottom to really familiarize myself with it. That was an interesting excercise but also a really valuable one in reading docs. You learn to kind of fill in the gaps yourself where the docs don't explain something perfectly well. 

One thing that mattered to me was preparing this module for distribution because I think too often I mess around on my computer locally and never actually have the experience of shipping code to production or putting it in front of other people. As such, I dug into [setuptools](http://setuptools.readthedocs.io/en/latest/) and learned about the various configurations  surrounding that module. I had to make choices about how I was going to deal with faulty user input during setup (I ended up using a while loop that re-prompts until satisfied), which also meant that my installation flow was more complicated than it would have been otherwise.

Lastly, it was a challenge to account for edge cases. Since my goal was always to be able to put it in front of other people, I wanted to account for scenarios in which users didn't provide perfect input. For example, what happens if the users directory name contains a space? What happens if they give a command to change their working directory but provide a filename instead of a directory? What happens if they reference their current directory by the commonly used "." and not its actual name? Those were things that I wanted to iron out, which led to a lengthy debug process once the bulk of the code had been written.

## Installation

Installation is most easily done using the setup.py file that can be found in this repository. However, installation does depend on the [Click library](https://github.com/pallets/click) for user configuration options (prompts for common file paths, favorite text editor, etc.). If you don't already have it installed, go ahead and install that before proceeding with the following command on the command line:

```
$ python3 setup.py
```

## Usage

The structure of all commands will be as follows:

```
$ ff [file or directory name] [-flag]
```
Note that every command works with both files and directories. If you issue a command that feels unnatural, such as changing directories to a file called helloWorld.js, the program will intelligently change to the directory in which helloWorld.js is located, since changing directories to helloWorld.js makes no sense.

There are 4 main flags you can use: --change-directory (aliased as -c), --open-editor (-e), --open-finder (-f), and --duplicated (-d).
Changing directories is fairly straightforward and can be done as follows:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/c.png "Changing Directories")
You'll notice that there's a folder on my Desktop called Find Me, which the program is able to find with ease, despite the fact that it's in a different directory from the one I'm currently in. It's also worth noting that my directory name had a space in it but was found regardless!

Opening a file or directory in your favorite editor has similar syntax, but with a flag -e:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/editor.png "Opening an editor")
During setup, I specified Atom as my text editor, so the directory opened in Atom automatically. And it contains a file called found.java! Cool!

Next, I can open any file or directory in a new window in the Mac Finder application using the flag -f:
![alt text](https://github.com/benhubsch/File-Finder/blob/master/pics/finder.png "Opening Mac Finder")
Again, we see the familiar found.java contained within the folder Find Me.

Lastly, you can add the duplicated flag to any command if you think there's a chance that you might have two or more files or directories of the same name in your file system. If you only have one, the program will assume that it's the one you want and will perform the relevant action like it would without the duplicated flag. If you have multiple, you will be given the opportunity to specify the file that you would like the action to be performed on.

Here is an example where I have a file called found.java that exists in multiple places, but I want to change my current working directory to one of them. I can use the -d flag in combination with the -c flag to achieve my desired result:
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

I would love any and all help with this project! I still need to make this compatible on operating systems besides OS X, and I think it'd be cool to clean up the setup process and make it pip installable. I also think it would be super \~fresh\~ if we incorporated autocomplete into it. Anybody want to make use of a Trie class that we can persist on a per-user basis? Create a branch, add commits, and [open a pull request](https://github.com/benhubsch/File-Finder/compare/).
