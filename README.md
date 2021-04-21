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
* Install make `sudo apt install make`
* Install GCC which is required for make command `sudo apt install gcc`
* Install Git `sudo apt install git`
* Clone this repository `git clone https://github.com/AlexHHsiao/linux.git`
* Navegate to cmpe-283/assignment1 directory
* Run `make` command. At this moment, you should see lots of file created. Make sure **cmpe283-1.ko** file exists
* Run `sudo insmod ./cmpe283-1.ko`command
* Run `dmesg` command. You should see the output
* In case you makes any change in **cmpe283-1.c**. Run `sudo rmmod cmpe283-1` and repeat above three steps
