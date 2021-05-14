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
### Hongquan Xiao
I worked on setting up the dev environment. I cloned this repository and built the kernel `make modules && make && sudo make modules_install && sudo make install`. 
I then installed Virtual Machine Manager inside of the VM and setup the inner VM.
I worked with Yizhou to understand the existing code and wrote test cases to test our changes.

### Yizhou Yan
I Worked with Hongquan to setup local enviroment for the assignment. Reviewed and standardlized the steps for building the linux kernel and completing the assignment.
Focused on editing cpuid.c file. Implemented leaf function in kvm_emulate.cpiud.
Discussed with Hongquan about the existing measurement code logic in svm.c.

## Steps to complete
* Make sure you are in this repository 
* Check your Linux version by running command `uname -a`
* Run command `cp /boot/config-YOUR-LINUX-VERSION-generic ./.config`
* Run command `make oldconfig` and keep pressing enter unit it finishes
* Make sure comment out `CONFIG_MODULE_SIG_ALL`, `CONFIG_MODULE_SIG_KEY`, and `CONFIG_SYSTEM_TRUSTED_KEYS` in newly created config file
* Run command `make modules && make && sudo make modules_install && sudo make install` to build and install Kernel
* Run command `sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager` to setup VM
* Create a new inner VM using Virtual Machine Manager which installed with above command. You can use ubuntu ISO or any other Linux images
* Create a test program and compile it in the new VM

## Question 3
Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there
more exits performed during certain VM operations? Approximately how many exits does a full VM
boot entail?

* The number of exits increase at a stable rate during certain VM operations.
* There are around four million exits a full VM boot entail.

---
# Assignment 3

## Code
[cpuid.c](/cmpe-283/assignment2/cpuid.c)
[vmx.c](/cmpe-283/assignment2/vmx.c)

## Team Member
### Hongquan Xiao
In the beginning, 
I worked on the code from assignment 2 and update vmx.c. I had some issue with my PC, so I reinstaslled VM and built the Kernel. I watched class recording and understood where to make the code change. I then made the change in vmx file to calculate the number of exits by using the atomic_inc function. I did research with Yizhou to understand each condition in cpuid. In the end after all code changes, I tested by using the inner VM and answered follow up question in assignment.

### Yizhou Yan
In this assignment, I mainly focused on the cpuid.c and vmx.c files.
Enabled system that responds to the numbers and frequency of each type exits when leaf function is invoked.
Thanks to Hongquan for helping me installed and built the Kernel and troubleshoot VM issuses.

## Steps to complete
* Copy the cpuid and vmx files into the location stated in assignment 2
* Refer to assignment for how to build kernel
* Make sure to reboot VM before go into the inner VM
* Create a test program and compile it in the inner VM


## Question 3
Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there
more exits performed during certain VM operations? Approximately how many exits does a full VM
boot entail?

* The number of exits increase at a stable rate during certain VM operations.
* There are around four million exits a full VM boot entail.

## Question 4
Of the exit types defined in the SDM, which are the most frequent? Least?
* Most frequent exit types: WRMSR, IO Instruction
* Least frequent exit types: WBINBD, MOV DR

---
# Assignment 4

## Team Member
### Hongquan Xiao
I worked on the assignment when the EPT was set to 0

### Yizhou Yan
Worked on EPT when it was set to 0.
## Question 2
Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
* with ept ![With EPT](/cmpe-283/assignment4/2.png)
* without ept ![Without EPT](/cmpe-283/assignment4/1.png)

## Question 3
What did you learn from the count of exits? Was the count what you expected? If not, why not?
The count is what I expected. The shadow paging approach is followed when the EPT is set to 0. The nested paging approach is followed when the EPT is not set to 0. There are three kinds of exits enabled, CR3 exits, page fault exits, and TLB flush exits during the shadow paging approach and causes the number of exits increases. Plus, The three kinds of exits occurs in the EPT violation which usually in the nested paging.

## Question 4 
What changed between the two runs (ept vs no-ept)?
For no-ept, the number of exits increases compares to ept.
