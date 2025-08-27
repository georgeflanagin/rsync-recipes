# rsync-recipes
Recipes for common operations with rsync

## Pre-requisites and installation

rsync has one hard boundary: the program must be installed on both computers if you are
using it to move or copy files between them. rsync is installed by default in most Linux
distros.

## Generally speaking, how does it work?

*Note:* the source and destination can most certainly be on the same computer. Unless we are discussing
specifics about single computer operations, the examples assume that two computers are involved.

The *source* computer is the one where the files already exist that you want to move or copy or otherwise
*synchronize*. The *destination* is the other computer. The general format for running rsync is:

```bash
rsync [options] source destination
```

The source does not need to be "here." You can copy files to your present login location or from it, but the
basic format of the command remains the same. In the recipes below, we will adopt the
names often used in cryptography, *alice* and *bob*. Alice will always be the source, and Bob will be the
destination.
