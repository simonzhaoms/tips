# Logging #

## Why ##

Unlike `print`, the standard Python package
[**logging**](https://docs.python.org/3/library/logging.html) can be
used to write something down without polluting the normal output
(`stdout` or `stderr`) and having to remove the logging code
afterwards.  It can also filter and redirect logs into different
places at will.


## Logging Level ##

There are [5
levels](https://docs.python.org/3/howto/logging.html#logging-levels)
of logging from the lowest severity to the highest:
* `logging.DEBUG`
* `logging.INFO`
* `logging.WARNING` (the default severity level)
* `logging.ERROR`
* `logging.CRITICAL`

Each of them corresponds to a logging function to output logs of that level:
* On the root logger (`logging.getLogger()`)
    + `logging.debug()`
    + `logging.info()`
    + `logging.warning()`
    + `logging.error()`
    + `logging.critical()`
* On an individual logger (`logging.getLogger(name)`)
    + `logging.Logger.debug()`
    + `logging.Logger.info()`
    + `logging.Logger.warning()`
    + `logging.Logger.error()`
    + `logging.Logger.critical()`

In addition, `logging.exception()` and `logging.Logger.exception()`
can be used to log a message with exception info and `logging.ERROR`
on the logger.  They should be called from an exception handler.


## A Simple Example ##

```python
import logging

# Use the root logger to log something.
logging.warning('This message will be printed to the console (stderr) by default')
logging.info('This message will not be printed by default since the default severity level is logging.WARNING.')
```

Actually, this is a **bad practice** to use the **root logger**
directly in your code.  `logging.basicConfig()` has the same side
effects as the above.

A **good practice** is always to use a **main logger** by calling
`logging.getLogger('xxx')` with a specific name `xxx`, and put all
submodules' logger under the hierarchy of `xxx`.

Why? As said in [Configuring Logging for a
Library](https://docs.python.org/3/howto/logging.html#configuring-logging-for-a-library),
it is good to attach a do-nothing handler to the top-level (main)
logger for a library:

```python
import logging
logging.getLogger('foo').addHanlder(logging.NullHandler())
```

Then if the users of the `foo` library configure their applications
under their own main loggers:

```python
import foo
import logging

logger = logging.getLogger('fooapp')
```

Thus the logs from the `foo` library will eventually end in its main
logger called `foo`.  If the users configure logging against the root
logger:

```python
import foo
import logging

logging.basicConfig(level=logging.DEBUG)
```

All logs, no matter whether it is from `foo` or `fooapp`, their logs
have chances to get to the root logger.


## Logging Flow ##

![https://docs.python.org/3/howto/logging.html#logging-flow](figure/logging_flow.png)

A log starts from a logging call such as `Logger.info()`, and will be
propagated as a
[`logging.LogRecord`](https://docs.python.org/3/library/logging.html#logrecord-objects)
instance up to higher layer (ancestor/parent) loggers
([`logging.Logger`](https://docs.python.org/3/library/logging.html#logger-objects))
to be filtered and handled by the their associated filters
([`logging.Filter`](https://docs.python.org/3/library/logging.html#filter-objects))
and
[handlers](https://docs.python.org/3/howto/logging.html#useful-handlers)
([`logging.Handler`](https://docs.python.org/3/library/logging.html#handler-objects))
until the root logger or the `propagate` attribute of a logger in the
route is set to `False`.
* A logger can be associated with a severity level, filters and
  hanlders.  A handler can also be associated with a severity level
  and filters.

  ```python
  import logging
  logger = logging.getLogger(__name__)
  logger.setLevel(logging.DEBUG)
  handler = logging.FileHandler()
  handler.setLevel(logging.DEBUG)
  formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
  handler.setFormatter(formatter)
  logger.addHandler(handler)
  ```

* The same logger named `xxx` can be obtained by calling
  `logging.getLogger('xxx')` from anywhere in the code.  A logger
  named `xxx.yyy` is the descendant/child logger of the logger named
  `xxx`.  Therefore, using `logging.getLogger(__name__)` in your
  modules makes the loggers automatically hierarchically organized.
  Actually, on the topest of the hierarchy is the hidden root logger,
  so that `root.xxx` and `root.xxx.yyy`.
* When processed in the starting logger, a log will go through the
  severity level, logger associated filter and logger associated
  handlers, respectively.  When processed in a parent logger, a log
  will only go through the handlers associated with the parent logger,
  without checking against the severity level of the parent logger,
  though the handlers of the parent logger have their own levels.
* That how the logs will look like is determined by the
  [`logging.Formatter`](https://docs.python.org/3/library/logging.html#formatter-objects)
  of the handler.  Available information of a log can be found from
  the [attributes of
  `logging.LogRecord`](https://docs.python.org/3/library/logging.html#logrecord-attributes),
  such as `filename`, `asctime`, `message`, `lineno` and `levelname`.


## Logging Configuration ##

Logging can be
[configured](https://docs.python.org/3/howto/logging.html#configuring-logging)
* [programmatically](https://docs.python-guide.org/writing/logging/#example-configuration-directly-in-code)
* through a [logging INI file using
  `logging.config.fileConfig()`](https://docs.python-guide.org/writing/logging/#example-configuration-via-an-ini-file)
* or a [logging dictionary using
  `logging.config.dictConfig()`](https://docs.python-guide.org/writing/logging/#example-configuration-via-a-dictionary)


## Good Practices ##

* Don't configure the root logger.  For example, do not directly use
  `logging.basicConfig()` and `logging.debug()`.  Always use
  `logging.getLogger('xxx')` with a proper logger name `xxx` such as
  `__name__`.  Use a top-level logger for your application/library and
  put all child loggers under it.
* Use `Handler.setLevel()` instead of `Logger.setLevel()`, so that you
  can use `Logger.setLevel()` when you needed.
* [`logging.RotatingFileHandler`](https://docs.python.org/3/library/logging.handlers.html#logging.handlers.RotatingFileHandler)
  is good for dealing with logs of large size.


## Reference ##

* Logging Documentation
    + [logging — Logging facility for Python](https://docs.python.org/3/library/logging.html)
    + [Logging HOWTO](https://docs.python.org/3/howto/logging.html)
    + [Logging Cookbook](https://docs.python.org/3/howto/logging-cookbook.html)
* [Understanding Python's logging module](https://www.electricmonk.nl/log/2017/08/06/understanding-pythons-logging-module/)
* [Hiding Sensitive Data from Logs with Python](https://relaxdiego.com/2014/07/logging-in-python.html)
* [Python Logging Tutorial](https://www.patricksoftwareblog.com/python-logging-tutorial/)
* [Good logging practice in Python](https://fangpenlin.com/posts/2012/08/26/good-logging-practice-in-python/)
