# How to refer an issue in a commit and close the issue automatically #

Putting a `\#` before a issue number can make GitHub knows we are
trying to refer an issue of a repo.  For example, you can refer to the
4th issue by `\#4`.

And GitHub also make it possible when we do that in a git commit
message.  So you can directly refer to the 4th issue in you git commit
message by `\#4`.

In addition, GitHub allows you close the issue just by putting an
extra keyword (such as `fix`, `resolve`, `close`) before the
reference.  For example, if your commit solves the issue `\#4`, you
can say `Fixed \#4: blah, blah`, then GitHub will automatically close
the 4th issue for you after you push this commit onto your GitHub
repo.

This also works when you submit a pull request (PR) that contains the
keyword followed by the reference to an issue.  Once your PR is
approved and merged into the branch, the issue will be automatically
closed.


## Reference ##

* [Closing issues using keywords](https://help.github.com/en/articles/closing-issues-using-keywords)
* [Closing Issues via Pull Requests](https://github.blog/2013-05-14-closing-issues-via-pull-requests/)
