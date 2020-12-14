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

## Steps followed for this assignment:
 Environment is brought up as per Assignment 2

 We changed the kernal code as per the requirement of Assignment 3. Files modified are cpuid.c and vmx.c. 

 Once the files are modified we built the module

 As only kvm related changes are done we built only the kvm module 
 ```
 sudo make -j 8 modules M=arch/x86/kvm
 ```
 First we remove the older modules 
 ```
 sudo rmmod kvm_intel
 sudo rmmod kvm
 ```

 After this do the below steps to insert the newly built modules

 ```
 sudo insmod arch/x86/kvm/kvm.ko
 sudo insmod arch/x86/kvm/kvm-intel.ko
 ```

 Now reboot the inner vm. Rebooting should take the updated changes and should reboot successfully

 Once innerVM is rebooted, open the terminal and run the below command.

 Ensure that cpuid is installed in the inner VM if it is not installed.

 ```
 cpuid -l 0x4ffffffd -s <exit_number>
 ```
 Give various exit numbers and check if the desired output is obtained.

 Case 1 :- For CPUID leaf node %eax=0x4FFFFFFE:
     Return the number of exits for the exit number provided (on input) in %ecx
     This value should be returned in %eax


     We can see the above outputs for some of these exit_numbers

     ```
     cpuid -l 0x4ffffffd -s 0
     cpuid -l 0x4ffffffd -s 1
     cpuid -l  0x4ffffffd -s 7 etc
     ```

Case 2 :- For leaf nodes 0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and 0xFFFFFFFF in %edx. 

    For exit numbers 35, 38, 42, 65, >=69

    ```
    cpuid -l 0x4ffffffd -s <exit_number>
    ```

    These exit numbers return 0 in eax, ebx, ecx and 0xFFFFFFFF in %edx. These exit numbers are not defined by the SDM. 

Case 3 :-  For exit types not enabled in KVM, return 0s in all four registers.

    For exit numbers 3, 4, 5, 6, 11, 16, 17, 33, 34, 51, 61

    ```
    cpuid -l 0x4ffffffd -s <exit_number>
    ```

    These exit numbers return 0 in all the below registers. These exit numbers are not enabled in KVM.


We wrote a shell script which would run for all the exit numbers and the output is captured. Also note that the value stored in these registers are in hexadecimal format.

The output of shell script




