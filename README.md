# VT-CMPE283-Assignment-3
Instrumentation through Hypercall

#### CMPE-283-Assignment-3
#### Group -
#### Deesha Desai - 015135536
#### Ananth Upadhya - 015234726

#### Assignment
Your assignment is to modify the CPUID emulation code in KVM to report back additional information when special CPUID leaf nodes are requested.



For CPUID leaf node %eax=0x4FFFFFFE:
Return the number of exits for the exit number provided (on input) in %ecx
This value should be returned in %eax


For leaf nodes 0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. For exit types not enabled in KVM, return 0s in all four registers.


#### Deesha Desai:
* Compiled the code with the required modifications
* Debugged and made changes to fix the errors which occurred while compiling the code
* Made required code changes to the cpuid.c and vmx.c files
* Created the documentation.

#### Ananth Upadhya:
* Made required code changes to the cupid.c and vmx.c files
* Investigated on how to perform testing for kernel code
* Wrote the test program and the shell script to execute cpuid command on all the exit number
* Updated the documentation


