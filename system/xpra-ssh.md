# Access a remote server with `ssh` and `xpra` together #


* [X forwarding by `ssh`](#x-forwarding-by-ssh)
* [Speed up X forwarding by `xpra`](#speed-up-x-forwarding-by-xpra)
* [Installation of `xpra`](#installation-of-xpra)
* [`xpra` usage examples](#xpra-usage-examples)
  + [`ml display rain`](#ml-display-rain)
  + [Open Pycharm](#open-pycharm)
  + [Reconnection](#reconnection)
* [Postscript](#postscript)

## X forwarding by `ssh` ##

[X forwarding](https://nnc3.com/mags/Networking2/ssh/ch09_03.htm)
allows you to run remote GUI application on your local machine.  `ssh`
X forwarding makes the communication secure by tunneling the X
protocol.  For example, after you type the following command on a
termianl locally:

```console
simon@local$ ssh -X remote  # ssh to remote machine with X forwarding enabled
simon@remote$ firefox       # Open Firefox Web Browser
```

a window of firefox browser opened on the remote will show on the
local machine.

However, `ssh` X forwarding may be very slow because of the network
latency.  One solution would be to compress the communication via:

```bash
ssh -X -C -c blowfish-cbc,arcfour user@host
```

However, the cipher `blowfish-cbc` and `arcfour` are not available in
**[OpenSSH](https://www.openssh.com)** anymore.  See
https://www.openssh.com/releasenotes.html.


## Speed up X forwarding by `xpra` ##

[`xpra`](https://xpra.org) is a command line tool that can be used to
 complement `ssh` X forwarding.  It is relatively latency-insensitive,
 thus can be used over worse links than standard X and faster.

`xpra` use a custom protocol to forward the display on the remote to
the local machine.  It also record the display for re-connecting from
another local machine.  From this point of view, `xpra` is similar to
[`byobu`](http://byobu.co), because you can connect the same display
from everywhere by `xpra`, just as you can log into the same terminal
session from everywhere by `byobu`.


## Installation of `xpra` ##

To use `xpra`, you have to install it on both the remote and your
local machine.  For example, on Ubuntu:

```bash
# see https://askubuntu.com/questions/1203609/how-to-add-xpra-repository-list

# install https support for apt (which may be installed already):
sudo apt-get update
sudo apt-get install -y apt-transport-https

# add Xpra GPG key
wget -q https://xpra.org/gpg.asc -O- | sudo apt-key add -

# add Xpra repository
sudo add-apt-repository "deb https://xpra.org/ $(lsb_release -cs) main"

# install Xpra package
sudo apt-get update
sudo apt-get install -y xpra
```

See [Repository Installation Instructions for Window
Switch](https://winswitch.org/downloads/) for instructions on other
systems.  **Window Switch** is a GUI front end for `xpra`.  However, I
think there are some bugs for Window Switch that makes it hard to use.


## `xpra` usage examples ##

### `ml display rain` ###

This example will show you how to 

1. Open a terminal session on the local machine (here we call it
   `s1`), type:

   ```console
   simon@local$ ssh remote            # ssh to the remote machine
   simon@remote$ xpra start :100      # Start a xpra session on a display numbered 100
   simon@remote$ export DISPLAY=:100  # Make sure subsequent GUIs show on the display 100
   simon@remote$ pip3 install mlhub   # Install mlhub -- The Machine Learning Hub
   simon@remote$ ml configure         # Configure mlhub
   simon@remote$ ml install rain      # Install the rain model in mlhub
   simon@remote$ ml configure rain    # Configure rain
   simon@remote$ ml display rain      # Display rain
   ```

   Nothing happens!? Wait util you finish the next step.

1. Open another terminal session on the local machine (we call it
   `s2`), type:

   ```console
   simon@local$ xpra attach ssh:remote:100  # Attach the local display to the remote display 100
   ```
   
   then some rain-related windows will be popped up right away on the
   local machine, which should be shown on the remote machine.  This
   is because you `export` your display on 100 and make `xpra` capture
   the display on 100, so when you `attach` via `xpra` on the display
   on 100, all visual things will show on the machine from which you
   start attaching.
   
1. When you finish using the remote machine, just `Ctrl+C` on session
   `s2` to dettach.  Finally, make sure you stop `xpra` before you
   shutdown the remote machine by `xpra stop :100` on session `s1`.


### Open Pycharm ###

There are two ways to open Pycharm locally via `xpra`:

1. The general way is to follow the steps in [the previous
   section](#ml-display-rain).

1. A more easy way is directly starting Pycharm with one command:

   ```console
   simon@local$ xpra start ssh:remote:100 --start=pycharm
   ```
   
   Then Pycharm will show on the local machine.  However, there may be
   an issue via `xpra`, so this way may fail.
   

### Reconnection ###

When you close the terminal where the above `xpra attach` are typed,
all the GUI windows attached to the remote display will disappear.
But you can still get them back again by typing `xpra attach
ssh:remote:100` in any machine, as long as the GUI windows are not
closed by mouse click and the processes are still running on the
remote machine.


## Postscript ##

- [NoMachine](https://www.nomachine.com) is a GUI tool can be used in
  similar way.  But I think it is not open source.

- Actually, you don't need to specify a display number when start
  `xpra`, since `xpra` will use 0 by default if 0 is not used.  And
  use the default display is better because you need not to stop it
  manually like`xpra stop :100`.  So I put the following into
  `~/.bashrc`:

  ```bash
  if ! xpra list | grep 'LIVE session at' > /dev/null; then xpra start; fi
  export DISPLAY=:0
  ```
  
  Then I just need to `xpra attach ssh:remote` without providing the
  display number to get the GUIs and there is no need to stop `xpra`
  manually before I shutdown the remote machine.

- Sometimes, `xpra` will not show the windows, then you can just
  re-attach.  Though there are some issues with `xpra`, I still think
  it is not an bad alternative to [X2Go](http://x2go.org).
