---
layout: post
title: Notes on C++
comment: true

---

## Introduction 

C++ is a compiled language. For a program to run, its source text has to be processed by a compiler, producing object files, which are combined by a linker yielding an executable program. A C++ program typically consists of many source code files (usually simply called source files). An executable program is created for a specific hardware/system combination; it is not portable,say, from a Mac to a Windows PC. When we talk about portability of C++ programs, we usually mean portability of source code.

A declaration is a statement that introduces a name into the program. It specifies a type for the
named entity:
- A type defines a set of possible values and a set of operations (for an object).
- An object is some memory that holds a value of some type.
- A value is a set of bits interpreted according to a type.
- A variable is a named object.
C++ offers a variety of fundamental types such as bool, char, int and double.

A char variable is of the natural size to hold a character on a given machine (typically an 8-bit byte), and the sizes of other types are quoted in multiples of the size of a char. The size of a type is implementation-defined (i.e., it can vary among different machines) and can be obtained by the sizeof operator; for example, sizeof(char) equals 1 and sizeof(int) is often 4.
