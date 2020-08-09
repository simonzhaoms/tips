# Parse command line arguments #

The most popular method of parsing command line arguments in Python is
to use Python package
[**argparse**](https://docs.python.org/3/library/argparse.html).

After we describe what arguments we expect and how they look like
through the functions provided by **argparse**, **argparse** can
figure out how to parse `sys.argv` --- the arguments passed from
command line, and will automatically generate help and usage messages
as well as issue errors given invalid arguments.

All command line arguments parsing programs using **argparse** should
have:

```python
import argparse                     # Import Python packge 'argparse'
parser = argparse.ArgumentParser()  # Create an ArgumentParser object

# Parse the arguments in 'sys.argv[1:]', and save the results into 'args'
args = parser.parse_args()
```

That is, all the descriptions of the argements are held in
[`argpase.ArgumentParser`](https://docs.python.org/3/library/argparse.html#argumentparser-objects)
and added by its methods.

## Content ##

* [Command line arguments](#command-line-arguments)
* [Sub-commands](#sub-commands)
* [Partial parsing](#partial-parsing)
* [multi-stage parsing](#multi-stage-parsing)


## Command line arguments ##

There are two kinds of command line arguments:

1. **Positional arguments**
    * Those are arguments without prefixing dashes `-`, such as
      `/home` in the command `ls /home`.
   
2. **Optional arguments**
    * Those are arguments with prefixing dashes `-`, such as `-l` in
      the command `ls -l /home` and `--help` in the command `ls
      --help`.
   
No matter what kinds of arguments, we use
[`argpase.ArgumentParser.add_argument()`](https://docs.python.org/3/library/argparse.html#the-add-argument-method)
to describe them:

```python
# myprogram.py
import argparse
parser = argparse.ArgumentParser(
        # Description of the program
    description='Process some integers.')

# Add argument specification

parser.add_argument(
      # Define a positional argument.
      # It will be referred as 'integers' after '.parse_args()'
    'integers',
      # Use 'N' to refer to 'integers' in the help message
    metavar='N',
      # It must be of type integer
    type=int,
      # It takes at least one parameter
    nargs='+',
      # Description of the argument in the help message
    help='an integer for the accumulator')

parser.add_argument(
      # Define a optional argument.
      # It will be referred as 'sum' after '.parse_args()'
    '--sum',
      # Rename this argument as 'accumulate'.
    dest='accumulate',
      # Define what to do when '--sum' is provided in the actual arguments.
      # 'store_const' means use the value of the 'const' argument below (which
      # is 'sum') if '--sum' is provided.  If not, use the value of the
      # 'default' argument below which is 'max'.
    action='store_const',
    const=sum,
    default=max,
      # Description of the argument
    help='sum the integers (default: find the max)')

# Parse command line argumets 'sys.argv[1:]'.
# 'parse_args()' is equivalent to 'parse_args(sys.argv[1:])'.
# 'args' will have two attributes, 'integers' and 'accumulate'.
# These attributes correspond to the two arguments described above.
args = parser.parse_args()

# 'args.accumulate' will be 'max' by default or 'sum' if '--sum' provided.
# 'args.integers' will be a list of integers provided in the command line
# arguments.
# Therefore, 'args.accumulate(args.integers)' will be max(...) or sum(...) if
# '--sum' is provided
print(args)
print('---------')
print(args.accumulate(args.integers))
```

If you run the script above:

```console
$ python myprogram.py --sum 1 2 3 4
```

then `sys.argv` will be `['myprogram.py', '--sum', '1', '2', '3',
'4']`, and `args = parser.parse_args()` is equivalent to `args =
parser.parse_args(['--sum', '1', '2', '3', '4'])`.

```console
$ python myprogram.py --help
usage: myprogram.py [-h] [--sum] N [N ...]

Process some integers.

positional arguments:
  N           an integer for the accumulator

optional arguments:
  -h, --help  show this help message and exit
  --sum       sum the integers (default: find the max)

$ python myprogram.py 
usage: myprogram.py [-h] [--sum] N [N ...]
myprogram.py: error: the following arguments are required: N

$ python myprogram.py abc
usage: myprogram.py [-h] [--sum] N [N ...]
myprogram.py: error: argument N: invalid int value: 'abc'

$ python myprogram.py 1
Namespace(accumulate=<built-in function max>, integers=[1])
---------
1

$ python myprogram.py 3 2 1
Namespace(accumulate=<built-in function max>, integers=[3, 2, 1])
---------
3

$ python myprogram.py 3 2 1 --sum
Namespace(accumulate=<built-in function sum>, integers=[3, 2, 1])
---------
6

$ python myprogram.py 3 --sum 2 1
usage: myprogram.py [-h] [--sum] N [N ...]
myprogram.py: error: unrecognized arguments: 2 1

$ python myprogram.py --sum 3 2 1
Namespace(accumulate=<built-in function sum>, integers=[3, 2, 1])
---------
6
```

If you have two arguments with `nargs='+'`, then the first arguments
will eat up all the provided parameters except for the last one:

```python
# myprogram2.py
import argparse

parser = argparse.ArgumentParser(description='Process some integers and strings.')
parser.add_argument('integers', metavar='N', nargs='+')
parser.add_argument('strings', metavar='S', nargs='+')

args = parser.parse_args()
print(args)
```

```console
$ python myprogram2.py 1 2 a b
Namespace(integers=['1', '2', 'a'], strings=['b'])
```

The order of defining arguments matters:

```python
# myprogram3.py
import argparse

parser = argparse.ArgumentParser(description='Process some integers and strings.')
parser.add_argument('strings', metavar='S', nargs='+')
parser.add_argument('integers', metavar='N', nargs='+')

args = parser.parse_args()
print(args)
```

```console
$ python myprogram3.py 1 2 a b
Namespace(integers=['b'], strings=['1', '2', 'a'])
```


## Sub-commands ##

Sub-commands like `git commit` or `ml install` can be implemented by
[`argparse.ArgumentParser.add_subparsers().add_parser()`](https://docs.python.org/3/library/argparse.html#sub-commands),
and their arguments can be added similarly by
`argparse.ArgumentParser.add_subparsers().add_parser().add_argument()`:

```python
# subcommands.py
import argparse

# Create a top level argument parser
parser = argparse.ArgumentParser()

# Add an argument for the top level parser
parser.add_argument('--foo', action='store_true', help='foo help')

# Create sub-command parsers for the top level parser
subparsers = parser.add_subparsers(help='sub-command help')

# Create a parser for the sub-command 'a'
parser_a = subparsers.add_parser('a', help='a help')
parser_a.add_argument('bar', type=int, help='bar help')

# Add default arguments for sub-command to dispatch action
parser_a.set_defaults(func=lambda x: x*2)

# Create a parser for the sub-command 'b'
parser_b = subparsers.add_parser('b', help='b help')
parser_b.add_argument('--baz', choices='XYZ', help='baz help')

# Add default arguments for sub-command to dispatch action
parser_b.set_defaults(func=lambda x: x.lower())

# Sub-commands are mutually exclusive, which means only one sub-command 
# is activated at a time, and only its corresponding arguments will be 
# considered as valid arguments if provided.
args = parser.parse_args()
print(args)
```

```console
$ python subcommands.py -h
usage: subcommands.py [-h] [--foo] {a,b} ...

positional arguments:
  {a,b}       sub-command help
    a         a help
    b         b help

optional arguments:
  -h, --help  show this help message and exit
  --foo       foo help

$ python subcommands.py
Namespace(foo=False)

$ python subcommands.py a
usage: subcommands.py a [-h] bar
subcommands.py a: error: the following arguments are required: bar

$ python subcommands.py b
Namespace(baz=None, foo=False)

$ python subcommands.py a 1
Namespace(bar=1, foo=False, func=<function <lambda> at 0x7f27899e0d08>)

$ python subcommands.py b 1
usage: subcommands.py [-h] [--foo] {a,b} ...
subcommands.py: error: unrecognized arguments: 1

$ python subcommands.py b --baz 1
usage: subcommands.py b [-h] [--baz {X,Y,Z}]
subcommands.py b: error: argument --baz: invalid choice: '1' (choose from 'X', 'Y', 'Z')

$ python subcommands.py b --baz X
Namespace(baz='X', foo=False, func=<function <lambda> at 0x7fc6cba22e18>)

$ python subcommands.py --foo b --baz X
Namespace(baz='X', foo=True, func=<function <lambda> at 0x7f005f188e18>)

$ python subcommands.py b --baz X --foo
usage: subcommands.py [-h] [--foo] {a,b} ...
subcommands.py: error: unrecognized arguments: --foo

$ python subcommands.py --baz b X
usage: subcommands.py [-h] [--foo] {a,b} ...
subcommands.py: error: unrecognized arguments: --baz X
```

If there are sub-commands defined, you must choose one of them:

```console
$ python subcommands.py c 1
usage: subcommands.py [-h] [--foo] {a,b} ...
subcommands.py: error: invalid choice: 'c' (choose from 'a', 'b')
```


## Partial parsing ##

If arguments passed are more than expected, `argparse` will produce an
error:

```console
$ python subcommands.py a 1 2
usage: subcommands.py [-h] [--foo] {a,b} ...
subcommands.py: error: unrecognized arguments: 2
```

If we want those extra arguments not to be considered,
[`argparse.ArgumentParser.parse_known_args()`](https://docs.python.org/3/library/argparse.html#partial-parsing)
can be used:

```python
# known.py
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--foo', action='store_true')

# The result of parse_known_args() will be a tuple of 2 elements.
# The first element is the result of known arguments.
# The second is a list of un-parsed arguments.
args = parser.parse_known_args()
print(args)
```

```console
$ python known.py
(Namespace(foo=False), [])

$ python known.py --foo abc 1
(Namespace(foo=True), ['abc', '1'])
```


## multi-stage parsing ##

See also [Sharing Parser
Rules](https://pymotw.com/3/argparse/index.html#sharing-parser-rules).


## Reference ##

* [argparse](https://docs.python.org/3/library/argparse.html)
* [Python Argparse Cookbook](https://mkaz.blog/code/python-argparse-cookbook/)
* [argparse -- Command-Line Option and Argument Parsing](https://pymotw.com/3/argparse/index.html)
* [Multi-level arg parse](https://gist.github.com/turtlemonvh/051e1034aa11cf2b3ae7fe30bf370dfe)
