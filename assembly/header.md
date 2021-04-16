---
title: header.asm
description:
toc: true
authors: []
date: 2021-04-12T17:13:24+05:00
lastmod: 2021-04-12T17:13:24+05:00
draft: false
weight: 1
---
Inside the header.asm file we have to include data that has to be included in the operating system binary. This is necessary so that the bootloader can understand that there is an operating system that can run on the machine. 

The header file contains the header start and end label. In between these labels lies the header data. Firstly, there is a magic number that the bootloader will look for. Next, we describe the architecture of the OS. “dd 0” means that the OS will start in protected mode. Next we calculate the length of the header programmatically by using the header tags. After this we enter the check sum and then finally the end tag.
 
 
 [My github repository link](https://github.com/anas-2000/CAO-assignment)