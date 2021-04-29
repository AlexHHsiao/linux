Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.

---

# Assignment 1

## Code
[cmpe283-1.c](/cmpe-283/assignment1/cmpe283-1.c)

## Output
![output1](/cmpe-283/assignment1/1.png)
![output2](/cmpe-283/assignment1/2.png)

## Team Member
Hongquan Xiao

## Steps to complete
* Install MV (VMware Workstation 16 in my case)
* Install Linux ISO [ubuntu](https://ubuntu.com/download/desktop)
* Open Linux and terminal
* Install make `sudo apt install make`
* Install GCC which is required for make command `sudo apt install gcc`
* Install Git `sudo apt install git`
* Clone this repository `git clone https://github.com/AlexHHsiao/linux.git`
* Navegate to **cmpe-283/assignment1** directory
* Run `make` command. At this moment, you should see lots of file created. Make sure **cmpe283-1.ko** file exists
* Run `sudo insmod ./cmpe283-1.ko`command
* Run `dmesg` command. You should see the output
* In case you make any change in **cmpe283-1.c**. Run `sudo rmmod cmpe283-1` command and repeat above three steps

---
# Assignment 2

## Code
[cpuid.c](/arch/x86/kvm/cpuid.c)
[vmx.c](/arch/x86/kvm/vmx/vmx.c)

## Team Member
Hongquan Xiao

## Steps to complete
* Make sure you are in this repository 
* Check your Linux version by running command `uname -a`
* Run command `cp /boot/config-YOUR-LINUX-VERSION-generic ./.config`
* Run command `make oldconfig` and keep pressing enter unit it finishes
* Make sure comment out `CONFIG_MODULE_SIG_ALL`, `CONFIG_MODULE_SIG_KEY`, and `CONFIG_SYSTEM_TRUSTED_KEYS` in newly created config file
* Run command `make modules && make && sudo make modules_install && sudo make install` to build and install Kernal
* Run command `sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager` to setup VM
* Create a new VM using Virtual Machine Manager which installed with above command. You can use ubuntu ISO or any other Linux images
* Create a test program and compile it in the new VM

