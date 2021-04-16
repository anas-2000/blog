---
title: print.c
description:
toc: true
authors: []
date: 2021-04-12T17:30:55+05:00
lastmod: 2021-04-12T17:30:55+05:00
draft: false
weight: 6
---
We create a “Char” struct to represent character— each character is represented by the ASCII character and an 8-bit color code. A buffer variable refers the video memory.   
**clear_row():**
Simply print an empty space for each column in a row.
**print_clear():**
Inside this function we loop through all the rows and in each iteration call the “clear_row()” function.
**print_char(char):**
If the character is a new line character or the current column is the last column, “print_newline()” is called. Otherwise the character is printed and current column is incremented.
**print_str(char*):**
Takes in a null terminated character array loops through it and prints a character in each iteration.
**print_newline():**
Simply sets the current column to 0. Next, it checks if it was the last row. If so, it moves each row up by 1 and so the first row is overwritten.
**print_set_color(foreground , background):**
Sets the foreground and background colour.


 [My github repository link](https://github.com/anas-2000/CAO-assignment)