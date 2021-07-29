<h1>C/C++</h1>

[TOC]

# Introduction

[Source-0](http://en.cppreference.com/w/)
[Source-1](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.3.0/com.ibm.zos.v2r3.cbclx01/toc.htm)
[Source-2](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.3.0/com.ibm.zos.v2r3.cbcsl01/toc.htm)
[Source-3](http://www.cplusplus.com/)


## The Features of C++ as a Language

- is an open ISO-standardized language.  
For a time, C++ had no official standard and was maintained by a de-facto standard, however since 1998, C++ is standardized by a committee of the ISO. Their page may be accessed [here](http://www.open-std.org/jtc1/sc22/wg21/).  

- is a compiled language.  
C++ compiles directly to a machine's native code, allowing it to be one of the fastest languages in the world, if optimized.  

- is a strongly-typed unsafe language.  
C++ is a language that expects the programmer to know what he or she is doing, but allows for incredible amounts of control as a result.  

- supports both manifest and inferred typing.  
As of the latest C++ standard, C++ supports both manifest and inferred typing, allowing flexibility and a means of avoiding verbosity where desired.  

- supports both static and dynamic type checking.  
C++ allows type conversions to be checked either at compile-time or at run-time, again offering another degree of flexibility. Most C++ type checking is, however, static.  

- offers many paradigm choices.  
C++ offers remarkable support for procedural, generic, and object-oriented programming paradigms, with many other paradigms being possible as well.  

- is _portable._  
As one of the most frequently used languages in the world and as an open language, C++ has a wide range of [compilers](http://www2.research.att.com/~bs/compilers.html) that run on many different platforms that support it. Code that exclusively uses C++'s standard library will run on many platforms with few to no changes.  

- is upwards compatible with C  
C++, being a language that directly builds off C, is compatible with almost all C code. C++ can use C libraries with few to no modifications of the libraries' code.  

- has incredible library support.  
A search for "library" on the popular project-management website [SourceForge](http://www.sourceforge.net) will yield over 3000 results for C++ libraries. A link to the results of the search may be found [here](http://sourceforge.net/directory/language:C%2B%2B/?q=library).

# Basic concepts
[Source-GCC](http://courses.cms.caltech.edu/cs11/material/c/mike/misc/compiling_c.html)
[Source-Compile-Cycle](https://www.cs.swarthmore.edu/~newhall/unixhelp/compilecycle.html)

## Compiler
Compiler compiles/translates all the source code into machine readable (raw binary/machine) code.
- creates a .o file (relocatable machine code for module func.c) from the output of the preprocessor
- can see the assembly code in `func.o` using either `objdump` or `gdb`

### Machine Code
- aka Raw binary code
- e.g.
    ```bash
    8B 0E 34 12
    ```

### Assembly Code
- Assembly is one level higher that is semi readable without having to memorize a bunch of hex or binary codes
- allows you to use symbolic names for addresses and do some simple math in creating the code.
- e.g.
    ```bash
    MOV CX, 1234H
    ```

## Linker
Linker links together a number of object files to produce a binary file which can be directly executed.
- creates an executable file (a.out file) from one or more .o files and .a or .so files (static or dynamic libraries)
- can use objdump (or in gdb the disass command) to disassemble the code in the executable

## Different kinds of files

### Source Code (.c/.cpp)
- contain function definitions

### Header Files (.h)
- contain function declarations (also known as function prototypes) and various preprocessor statements
- used to allow source code files to access externally-defined functions

### Object Files (.o/.obj)
- (output of compiler & input to the linker)
- These files are produced as the output of the compiler
- consist of function definitions in binary form
- are not executable by themselves
- Object files end in ".o" by convention
- can see the assembly code in `func.o` using either `objdump` or `gdb`

### Binary Executable
- (output of linker & executable with resolved reference)
- produced as the output of a program called a "linker"
- linker links together a number of object files to produce a binary file which can be directly executed
- have no special suffix on Unix operating systems (or .out default suffix)
- have .exe suffix on Windows operating systems
- generates assembler output (a.out, default name)

### Library Files (.a)
- files are archives
- are groups of objects or static libraries
- input to the linker
- similar to the .jar or .dll files

### Shared Library Files (.so)

## Preprocessor
- Before the C compiler starts compiling a source code file, the file is processed by a preprocessor
- automatically invoked by compiler before compilation
- expands the source code file by incorporating the pre-processor files (#include <.h/.c/.cpp>) included in the source code
    - either it creates a real file
    - or creates modified source code in memory for short time before being sent to the compiler
    
### Preprocessor Directives
- Declarative
    - #define
        - mainly used to define constants
        ```c
         #define BIGNUM 1000000
        ```
    - #include
        - used to access function definitions defined outside of a source code file
        ```c
        #include <stdio.h>
        #include "somelocalcode.h"
        ```
        
        or
        
        ```c
        #include "somelocalcode.c"
        ```
        
- Conditional
    - #if, #elif, #else, #ifdef, #ifndef, #endif
    
## GNU Compile Collection (GCC)    
- aka GNU C Compiler

### Compile using gcc

#### Background
- Lets say func.h have a function declarations : hello()
    - and we are defining it in func.c file (func.c does not have main() function)
        - now want to use the hello() function in source.c, so we can include
            - func.h file, or
            - func.c file (BAD IDEA)


#### Flow
- func.c & source.c both need `#include "func.h"`, because
    - func.c is defining the code which backs the hello() function
    - source.c is using/calling the hello() function and invoking its behavior, so it has to know the behavior & memory size need to allocate for the same
        - but it does not need the actual definition/implementation of hello() yet
- the compiler will generate .o (object file, compiled but not executable) file
    - func.o from func.c, and
    - source.o from source.c which includes main method and unresolved reference of hello() function
    ```bash
    gcc -c func.c
    gcc -c source.c
    ```
    
- here, func.o & source.o  are not self executable because
    - func.o doesn't have main() , and
    - source.o have one un-resolved reference
- now, comes the `linker`
    - linker will combine the two object files `func.o` & `source.o` into an executable file
    - now it connects the dot between both the object files & resolves the un-resolved reference
    - now, at run time, program can jump to the correct location
    
    ```bash
    gcc func.o source.o -o program

    ```
    
### gcc Misc

#### is there any need to compile the .h files?
No.

#### How to organize things between .h files and .c/.cpp file?
- Put as much as you can in the .c and as little as possible in the .h. 
- The includes in the .c are only included when that one file is compiled, but the includes for the .h have to be included by every file that uses it.

#### Should is include/import .c/.cpp file instead .h because it just works fine?
No. Lets say .c file has definition of class `Foo` &  this .c/.cpp file are used/referenced by multiple source code files (compilation units), then those all source code files will have definition of class `Foo` multiple times and which may cause a problem because linker will get confused and throw error.

# C++ Keywords

# Expressions
## Operators
- Arrow `-->`: Used to access classes, structure, or union member using pointer.
    - e.g.
    ```c
    
    ```
- Dot `.`: Used to access classes, structure, or union member.
    - e.g.
    ```c
    
    ```
- Scope Resolution `::` : Qualifies the abstracted/hidden member/names
    - e.g. 
    ```c
    int count = 0;

    int main(void) {
      int count = 0;
      ::count = 1;  // set global count to 1
      count = 2;    // set local count to 2
      return 0;
    }
    ```
    
# Declaration
## Function definition
## Template declaration
## Explicit template instantiation
## Explicit template specialization
## Namespace definition
## Linkage specification
- extern "C" is a linkage-specification

## Attribute declaration (attr ;) (since C++11)
## Empty declaration (;) (since C++11)
##  A function declaration without a decl-specifier-seq:
## Specifiers
### Declaration Specifiers
- typedef: typedef is used to give data type a new name
    - e.g.
    ```c
    typedef unsigned char BYTE;
    ```
    
### Type Specifiers
- `class` ABC
- `enum` Abc
- `char` name

## Declarators

# Initialization

# Functions
## In-built
- strncpy(): char * strncpy ( char * destination, const char * source, size_t num );
    - copies characters from string

## Lambda


## Pass by Value

## Pass by Reference

# Statements
## Expression Statements
## Compound Statements
## Selection Statements
## Label Statements
## Iteration Statements
## Jump Statements
## Declaration Statements
## Try Blocks
## Atomic and Synchronized Blocks

# Classes

# Templates

# STL (Standard Template Library)

- The Standard Template Library (STL) is a set of C++ template classes to provide common programming data structures and functions such as lists, stacks, arrays, etc. 
- It is a library of container classes, algorithms and iterators.

# Exceptions



# Misc
## namespace vs include
https://stackoverflow.com/questions/389922/c-namespace-and-include



# REST API
- https://msdn.microsoft.com/en-us/magazine/dn342869.aspx


# Microservice Based on REST
- https://medium.com/audelabs/modern-c-micro-service-implementation-rest-api-b499ffeaf898
- https://martinfowler.com/articles/microservices.html
- https://dev.otto.de/2016/03/20/why-microservices/
