# `fasd` -- For faster folder and file jump #

[`fasd`](https://github.com/clvv/fasd) can be used to jump or switch
  between frequently used folders or files with less typing.  It
  supports case-insensitive matching as well as fuzzy name matching.

`fasd` stands for its 4 aliases:
- **f** for file.
- **d** for directory.
- **a** for all, that is both file and directory.
- **s** for show, that is showing a list for selection.


* [Installation](#installation)
* [Safe usage](#safe-usage)
* [Usage with caution](#usage-with-caution)


## Installation ##

```console
$ git clone https://github.com/clvv/fasd.git
$ cd fasd
$ sudo make install
$ echo 'eval "$(fasd --init auto)"' >> .bashrc
```


## Safe usage ##

Feel free to use it.

```bash
# List frequently visited files or directories whose names contain 'bar' and paths contain 'foo'
sa foo bar
sf foo bar    # List files only
sd foo bar    # List directories only
a foo bar     # Print out the most frequently visited file and directory
f foo bar     # Print out only the file
d foo bar     # Print out only the directory

# List frequently visited files or directories whose paths contain 'foo' and 'bar'
sa foo bar /
sf foo bar /  # List files only
f foo bar /   # Print out only the most frequently visited file

# List frequently visited files or directories whose names are postfixed with 'bar' and paths contain 'foo'
sa foo bar$

# Jump to frequently visited directories whose paths contain 'foo'.
# If there are more than one, a list of possible folders will be printed for selection.
zz foo /
z foo /     # Jump into the most frequently visited folder
```


## Usage with caution ##

There may be some problems with the following usages.  See
clvv/fasd#134.

```bash
# List frequently visited files, whose names contain 'foo', for selection, and open it with gedit.
# Equivalent to: $ sf -e gedit foo
gedit `sf foo`

# Copy 'foo' to the frequenly visited directories whose name conttain 'mlhub' and paths contain 'site'.
# If there are multiple choices, a list of them will be printed out for selection.
cp foo `sd site mlhub`
```

For example, if there is no directory called `sd site mlhub`, then:

```bash
cp a b `sd site mlhub`
```

will become:

```bash
cp a b
```

Similarly, 

```bash
mv a b `sd site mlhub`
```

will become:

```bash
mv a b
```
