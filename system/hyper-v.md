# Hyper-V #

* [What is Hyper-V](#what-is-hyper-v)
* [Installation](#installation)
* [Create a Virtual Machine](#create-a-virtual-machine)
* [Reference](#reference)


## What is Hyper-V ##

Hyper-V is just like other hypervisor (such as VirtualBox, VMWare)
that allows you to create a virtual machine in your Windows system.
But Hyper-V is part of Windows.


## Installation ##

To use Hyper-V, Your OS must be Windows 10 Enterprise, Pro or
Education.  Your CPU should be 64-bit with Second Level Address
Translation (SLAT), and support for VM Monitor Mode Extension (VT-x on
Intel CPUs), which means you need to enable VT-x in your system BIOS
or UEFI.

Go to 'Turn Windows Features On or Off' (`Control Panel` -> `Programs`
-> `Programs and Features`), tick on the box 'Hyper-V' to install
Hyper-V and reboot.


## Create a Virtual Machine ##

1. Open 'Hyper-V Manager'.

1. Click 'Quick Create' in 'Hyper-V Manager' to download a
   pre-customized virtual machine such as Ubuntu 18.04.02 LTS.  And
   follow the instruction to install.
   

### Note ###

1. I recommend to use 'Quick Create' to create a virtual machine
   instead of 'New'.  Otherwise, you need to do a lot of manual
   configuration to make it run side by side with your Windows host
   seamlessly.
   
1. If you do use 'New' and if `Security` -> `Secure Boot` is selected
   in the VM settings, make sure 'Microsoft UEFI Certificate
   Authority' is the template being used.
   
1. Be default, the VM you created have no access to the Internet.  You
   need to create a Virtual Switch via 'Virtual Switch Manager', and
   select the Virtual Switch you created in the Network Adapter
   setting of the VM.


## Reference ##

* [Introduction to Hyper-V on Windows 10](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)
* [Step-By-Step: Enabling Hyper-V for use on Windows 10](https://techcommunity.microsoft.com/t5/ITOps-Talk-Blog/Step-By-Step-Enabling-Hyper-V-for-use-on-Windows-10/ba-p/267945)
