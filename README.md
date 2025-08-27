# rsync-recipes
Recipes for common operations with rsync

### Pre-requisites and installation

rsync has one hard boundary: the program must be installed on both computers if you are
using it to move or copy files between them. rsync is installed by default in most Linux
distros.

### Generally speaking, how does rsync work?

The *source* computer is the one where the files already exist that you want to move or copy or otherwise
*synchronize*. The *destination* is the other computer. The general format for running rsync is:

```bash
rsync [options] source destination
```

The source and the destination can be on the same computer, in which case rsync behaves like cp and mv with 
more flexibility and greater speed.

The source does not need to be "here." You can copy files to your present login location or from the source, but the
basic format of the command remains the same. In the recipes below, we will adopt the
names often used in cryptography, *alice* and *bob*. Alice will always be the source, and Bob will be the
destination. Except when called out, Alice will be our login computer; i.e., where we are.

### With no options, what are the defaults?

By default, ...

- rsync does not recursively go through a directory tree.
- rsync does not follow symbolic links -- it only copies the links as links.
- rsync does not provide a narrative of its progress; it is quiet.
- rsync does not consider any metadata except for a file's [1] name, [2] size, and [3] modification time. The
  modification time is the one you see with `ls -l`.

### What are the most common options?

`-r` : recursively traverse the directory mentioned as the source.

`-a` : as with `-r`, but set the time stamps on the files at the destination to match the source. Useful for backups.

`-v` : provide a haemorrhagic narrative of what's going on, as it happens. Something to keep in mind: if you are
using rsync to move several terabytes of data, this file is going to be *huge*.

`--dry-run` : essential for debugging, rsync can tell you what the command would do without really doing anything except for telling you.

`-n` : same thing as `--dry-run`, but harder to spot in a script.

### What are the most dangerous options?

`--remove-source-files` : the option turns "copy" into "move"

`--delete` : There are many flavors of `--delete`, and they remove files at the destination that are not referenced in the rsync command.

## The recipes

### Copy one file from alice to bob.

`rsync myfile bob:~/.`

myfile will appear at `bob:~/myfile`.

### Copy a file from bob to alice.

`rsync bob:~/myfile .`

### Copy files using a wildcard file name

`rsync myfiles* bob:~/.`

### Copy a directory and the files in it, creating the directory at the destination.

`rsync -a mydir bob:~/`

### Copy the contents of a directory to a directory at the destination 

`rsync -a mydir/ bob:~/somedir`

### Synchronize a directory on Alice with a directory on Bob

`rsync -a --delete mydir bob:~/`
