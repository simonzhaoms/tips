# Run External programs with **subprocess** #

The standard Python library
[**subprocess**](https://docs.python.org/3/library/subprocess.html)
can be used to run external programs.


## `subprocess.run()` ##

```
subprocess.run(
    args, *, stdin=None, input=None, stdout=None, stderr=None,
    capture_output=False, shell=False, cwd=None, timeout=None,
    check=False, encoding=None, errors=None, text=None,
    env=None, universal_newlines=None, **other_popen_kwargs)
```

**NOTE**: From Python 3.5 on, `subprocess.run()` combines all the
functionality of older functions `subprocess.call()`,
`subprocess.check_call()`, `subprocess.check_output()`.  Beneath all
the functions, a `subprocess.Popen` object is used.

The arguments of `subprocess.run()` is almost the same as the
constructor of `subprocess.Popen`.  So for general purpose,
`subprocess.run()` is preferred, and `subprocess.Popen` is used for
finer control.

The first argument `args` of `subprocess.run()` is a string or a list
of strings with its first element being the command to run.
* If `args` is a string and the argument `shell=False` (by default),
  `args` should be the command without any options.
* If `shell=True`, storing the command with its options together as a
  single string into `args` instead of a list of strings will enable
  shell's features such as variable expansion on the command.

To capture output of the command, set `capture_output=True`, thus
`stdout=subprocess.PIPE` and `stderr=subprocess.PIPE` will be set
automatically, and the output will be stored in the returned
`subprocess.CompletedProcess` object
(`subprocess.CompletedProcess.stdout` and
`subprocess.CompletedProcess.stderr`) from `subprocess.run()`.
Otherwise, the output will be printed on the console by default.

To enable exception raising, set `check=True`, thus a
`subprocess.CalledProcessError` exception holding the exit code
(`subprocess.CalledProcessError.returncode`) and output
(`subprocess.CalledProcessError.output`,
`subprocess.CalledProcessError.stdout` and
`subprocess.CalledProcessError.stderr`) will be raised when the
command fails.


```python
import subprocess

try:
    result = subprocess.run('cat xxx', shell=True, check=True, capture_output=True)
except CalledProcessError as e:
    print(e.stderr.decode('utf-8'))
    return

print(result.stdout.decode('utf-8'))
```

## `subprocess.Popen` ##

```python
class subprocess.Popen(
    args, bufsize=-1, executable=None,
    stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=True,
    shell=False, cwd=None, env=None, universal_newlines=None,
    startupinfo=None, creationflags=0, restore_signals=True,
    start_new_session=False, pass_fds=(), *,
    encoding=None, errors=None, text=None)
```

```python
import subprocess

# 
with subprocess.Popen(['ls', '-l'], stdout=subprocess.PIPE, stderr=subprocess.PIPE) as proc:
    print(proc.stdout.read().decode('utf-8'))

# Or
proc = subprocess.Popen(['ls', '-l'], stdout=subprocess.PIPE, stderr=subprocess.PIPE)

try:
    out, err = proc.communicate()
except CalledProcessError as e:
    print(e.stderr.decode('utf-8'))
    return

print(out.decode('utf-8'))
```


## Reference ##

* [Subprocess Documentation](https://docs.python.org/3/library/subprocess.html)
* [Python Subprocess Module - Running external programs](https://crashcourse.housegordon.org/python-subprocess.html)
* [Globbing and Python's "subprocess" module](https://lerner.co.il/2017/07/20/globbing-pythons-subprocess-module/)
* [Writing to a python subprocess pipe ](https://gist.github.com/waylan/2353749)
* [Some example for subprocess.Popen exception example](https://gist.github.com/s4553711/9488399)
