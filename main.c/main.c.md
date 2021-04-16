---
title: main.c
description:
toc: true
authors: []
date: 2021-04-12T17:31:35+05:00
lastmod: 2021-04-12T17:31:35+05:00
draft: false
weight: 4
---
 In here, we have create a “kernel_main()” function which is called in the main64.asm file. Inside the main.c file we call a bunch of functions:
-	print_clear()— to clear the screen
-	print_set_color(foreground_color, background_color)— to set foreground and background color.
-	print_str(string)— to print text.


 [My github repository link](https://github.com/anas-2000/CAO-assignment)