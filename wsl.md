# Windows Subsystem for Linux (WSL) #

* [What is WSL](#what-is-wsl)
* [How does WSL Work](#how-does-wsl-work)
* [Installation](#installation)
  + [Prerequisites](#prerequisites)
  + [Install WSL](#install-wsl)
  + [Install a Linux Distro](#install-a-linux-distro)
* [Usage](#usage)
  + [Launch WSL](#launch-wsl)
  + [Interaction with Windows](#interaction-with-windows)
* [Misc](#misc)
  + [File System](#file-system)
  + [Uninstallation](#uninstallation)
* [Reference](#reference)


## What is WSL ##

[**WSL** -- the Windows Subsystem for
Linux](https://docs.microsoft.com/en-us/windows/wsl/about), was
intrudoced in 2016.  It was called Bash on Ubuntu on Windows back
then.  It is a component in Windows that makes you can run Linux
commmands (Linux binary executables) directly in Windows.  It looks
like a virtual machine but without the overhead of it.

The primary purpose of WSL is to make the Linux command-line tools can
be run in Windows and interact with other Windows command-line tools.


## How does WSL Work ##

The request for a Linux system call from any Linux applications in WSL
will be translated by a Linux kernel compatibility layer into a
request of Windows kernel calls.  So it looks like a command-line
Linux distro without the actual Linux kernel but a Linux kernel
compatibility layer in Windows.

It is different from Cygwin, because Cygwin provides Cygwin runtime
running in user mode to do the translation, and all Linux application
needs to be rebuilt from source and linked to Cygwin runtime to be
used in Windows.


## Installation ##

### Prerequisites ###

To use WSL, your OS must be Windows 10 version 1709 or the latest

### Install WSL ###

Go to 'Turn Windows Features On or Off' (`Control Panel` -> `Programs`
-> `Programs and Features`), tick on the box 'Windows Subsystem for
Linux' to install WSL and reboot.

Or run the command below in PowerShell as administrator:

```ps1con
PS> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

### Install a Linux Distro ###

Then you also need to go to Microsoft Store and search for a Linux
distro (for example, Ubuntu) to install.


## Usage ##

### Launch WSL ###

To Launch WSL, you can launch the installed Linux distro from Windows
Start menu.

You can also launch it from PowerShell (Below I use `PS>` to indicate
PowerShell and `$` to indicate Linux command line in WSL):

```ps1con
PS> ubuntu  # Launch Ubuntu
PS> debian  # Or launch Debian
PS> wsl     # Launch the default distro
```

Then you are inside WSL command line environment, where you can run
Linux commands just like in a Linux machine:

```console
$ ls -a
.  ..  .bash_history  .bash_logout  .bashrc  .profile  .sudo_as_admin_successful
```

### Interaction with Windows ###

* Other than launching and run Linux commands inside a WSL distro, you
  can also run the commands directly in Windows without going into the
  distro first:
  
  ```ps1con
  PS> wsl ls -a
  .  ..  .bash_history  .bash_logout  .bashrc  .profile  .sudo_as_admin_successful
  ```

* You can also feed the output from a Windows command to a Linux
  command, and vice versa:
  
  ```ps1con
  PS> ipconfig | wsl grep IPv4  # Pipeline Windows and Linux command in PowerShell
     IPv4 Address. . . . . . . . . . . : 10.168.2.39
     IPv4 Address. . . . . . . . . . . : 192.168.139.81
  PS> wsl                       # Launch WSL
  $ ipconfig.exe | grep IPv4    # Pipeline Windows and Linux command in WSL
     IPv4 Address. . . . . . . . . . . : 10.168.2.39
     IPv4 Address. . . . . . . . . . . : 192.168.139.81
  ```
  
  **Note**: Windows command should be appended with `.exe` extension
  if run in WSL.


## Misc ##

### File System ###

* In WSL, all Windows drives are mounted under `/mnt`.  To access the
  files under Windows' C or D drive, you can `cd /mnt/c` or `cd
  /mnt/d` in WSL.  To modify files in Windows from WSL, you need to
  run WSL as administrator other than as sudo.  The mounted Windows
  file system is DriveFs in WSL, and the Linux file system is VolFs in
  WSL.
  
* In Windows, all Linux file systems are in a directory like

  ```
  C:\Users\<username>\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\
  ```
  
  You can also open current working directory in WSL by executing `$
  explorer.exe .`.  But be aware that modifying Linux files within
  Windows would have side effects, because some functionalities of
  Linux don't have similar counterparts in Windows, such as file mode,
  which would lead to inconsistencies in the file attributes when
  modified in Windows.


### Uninstallation ###

To uninstall one of the installed distros, you can right-click the
distro in Windows Start menu to uninstall it.  But then if you want to
reinstall it, you need to remove the installed directory of previous
installation, such as

```
C:\Users\<username>\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\
```


## Reference ##

* [Windows Command Line Tools For Developers](https://devblogs.microsoft.com/commandline/)
* [Windows Subsystem for Linux Documentation](https://docs.microsoft.com/en-us/windows/wsl/about)
* [Microsoft/WSL -- GitHub](https://github.com/Microsoft/WSL)
* [Bash On Ubuntu On Windows](https://github.com/abergs/ubuntuonwindows)
* [A community powered list of programs that work (and those that don't) on the Windows subsystem for Linux](https://github.com/ethanhs/WSL-Programs)
* [sirredbeard/Awesome-WSL](https://github.com/sirredbeard/Awesome-WSL)
* [Windows Subsystem for Linux Blog](https://blogs.msdn.microsoft.com/wsl/)
