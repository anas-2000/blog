---
title: main.asm
description:
toc: true
authors: []
date: 2021-04-12T17:13:11+05:00
lastmod: 2021-04-12T17:13:11+05:00
draft: false
weight: 2
---
The main.asm file acts as an entry point for the operating system. Initially we code it for 32-bit mode, but later we make another for 64-bit mode. Therefore, we set the bits to 32.

The first step in converting the OS to 64 bit mode is to set up a stack in the main.asm file. We reserve a 16 KB of space for the stack. We include the stack in the “bss” section. Since the CPU uses the ESP register to determine the address of the current stack frame, we store the address of stack top in this register, since the stack is empty initially. We have to switch the kernel into 64 bit mode, and to do this the CPU must be switched to the “long mode”. So we first have to check whether the CPU supports the long mode.

First, the “check_multiboot” function is called. This function confirms that the OS has been loaded by a multiboot2 bootloader. Then “cpu_id” is called which provides CPU information. After this, “check_long_mode” is called which checks for the long mode support using cpu_id. These subroutines are described below.

**check_multiboot:**  
First we check whether the EAX register contains what is called a “magic value”. If the EAX register does not contain  the magic value, we jump to the “no_multiboot” label and an error message will be displayed, which means that there is no multiboot support. In case EAX does contain the magic value, we will simply return from the sub routine. To print the error we load the error message in the video memory. The mov instructions under the “error” label do exactly that.

**check_cpu_id:**  
We have to flip the id bit of the FLAGS register. If the id bit is successfully flipped, it means that the CPU supports cpuid. Otherwise it does not support cpuid. We copy the flags register into EAX, by pushing the flags register onto the stack (using pushfd) and then popping it (using pop EAX). We also copy it into EAX for comparison. The “id” bit is bit 21. So we perform XOR on the bit 21 in the EAX which is the “id” bit. Next we copy this into the flags register and back to EAX. The reason of copying to flags register from EAX and then copying the flags register back to EAX is to check whether the CPU has reversed the id bit. If the CPU has reversed the id bit it means that CPU id is not supported, otherwise the CPU supports CPU id. Hence, we compare EAX with ECX. If they match, it means that the CPU has reversed the id bit, and therefore we jump to no_cpuid label and print an error.

**check_long_mode:**  
Firstly, we have to confirm whether the cupid supports extended processor info. So we move 0x80000000 into EAX and then call cupid which implicitly takes EAX as an argument. If the CPU supports cpuid it stores a number back to EAX which is greater than the number initially in EAX(0x80000000). So we compare EAX with 0x80000001, and if the value in EAX is less than this, it means that the extended processor info is not supported and hence long mode is not supported. In this case we jump to the “no_long_mode” label and display an error. 
Otherwise we use the extended processor info to check whether the long mode is supported. To do this, we move 0x80000001 into EAX and call cpuid. This time cpuid stores a value into EDX and if the  bit 29 is set it means that the long mode is supported.  So we test the bit 29 of EDX. If it is not set, long mode is not supported and hence we will jump to the “no_long_mode” label.  
  
Till now we have checked whether the CPU supports long mode, but in order to enter the 64-bit long mode, we must implement virtual memory through paging. To do this we call two subroutines in the main.asm file: “setup_page_tables” and “enable_paging”. 
In the .bss section we reserve 4 KB for page tables level 4, level3 and level 2. 


[My github repository link](https://github.com/anas-2000/CAO-assignment)