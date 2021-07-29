<h1>Software Engineering</h1>

<h3>Table of Contents</h3>

[TOC]

# Programming Languages

## An Overview of Programs and Programming Languages

In order to better communicate to our computers what exactly it is we want them to do, we've developed a wide range of **programming languages** to make the communication process easier.  

Depending on the type of project, there are many factors that have to be considered when choosing a language. Here is a list of some of the more noteworthy ones:  

###   Compiled, interpreted, or JIT-compiled  
**Compiled languages** are translated to the target machine's native language by a program called a compiler. This can result in very fast code, especially if the compiler is effective at optimizing, however the resulting code may not port well across operating systems and the compilation process may take a while.  
**Interpreted languages** are read by a program called an interpreter and are executed by that program. While they are as portable as their interpreter and have no long compile times, interpreted languages are usually _much_ slower than an equivalent compiled program.  
Finally, **just-in-time compiled** (or JIT-compiled) languages are languages that are quickly compiled when programs written in them need to be run (usually with very little optimization), offering a balance between performance and portability.  

###   High or Low Level Level
In this case, refers to how much the nature of the language reflects the underlying system. In other words, a programming language's level refers to how similar the language is to a computer's native language. The higher the level, the _less_ similar it is.  
A **low-level language** is generally quite similar to machine code, and thus is more suitable for programs like device drivers or very high performance programs that really need access to the hardware. Generally, the term is reserved for machine code itself and assembly languages, though many languages offer low-level elements. Since a low-level language is subject to all the nuances of the hardware it's accessing, however, a program written in a low-level language is generally difficult to port to other platforms. Low level languages are practically never interpreted, as this generally defeats the purpose.  
A **high-level language** focuses more on concepts that are easy to understand by the human mind, such as objects or mathematical functions. A high-level language usually is easier to understand than a low-level language, and it usually takes less time to develop a program in a high-level language than it does in a low-level language. As a trade-off one generally needs to sacrifice some degree of control over what the resulting program actually does. It is not, however, impossible to mix high-level and low-level functionality in a language.  

###   Type System  
A **type system** refers to the rules that the different types of variables of a language have to follow. Some languages (including most assembly languages) do not have types and thus this section does not apply to them. However, as most languages (including C++) have types, this information is important.  

*   **Type Strength: Strong or Weak**  
A strong typing system puts restrictions on how different types of variables can be converted to each other without any converting statements. An ideal strong typing system would forbid implicit "casts" to types that do not make any sense, such as an integer to a Fruit object. A weak typing system would try to find some way to make the cast work.  

*   **Type Expression: Manifest or Inferred**  
This deals with how the compiler/interpreter for a language infers the types of variables. Many languages require variables' types to be explicitly defined, and thus rely on manifest typing. Some however, will infer the type of the variable based on the contexts in which it is used, and thus use inferred typing.  

*   **Type Checking: Static or Dynamic**  
If a language is statically typed, then the compiler/interpreter does the type checking once before the program runs/is compiled. If the language is dynamically type checked, then the types are checked at run-time.  

*   **Type Safety: Safe or Unsafe**  
These refer to the degree to which a language will prohibit operations on typed variables that might lead to undefined behavior or errors. A safe language will do more to ensure that such operations or conversions do not occur, while an unsafe language will give more responsibility to the user in this regard.  

These typing characteristics are not necessarily mutually exclusive, and some languages mix them.  

###   Paradigms  
A programming paradigm is a methodology or way of programming that a programming language supports. Here is a summary of a few common paradigms:  

*   **Declarative**  
A declarative language will focus more on specifying what a language is supposed to accomplish rather than by what means it is supposed to accomplish it. Such a paradigm might be used to avoid undesired side-effects resulting from having to write one's own code.  

*   **Functional**  
Functional programming is a subset of declarative programming that tries to express problems in terms of mathematical equations and functions. It goes out of its way to avoid the concepts of states and mutable variables which are common in imperative languages.  

*   **Generic**  
Generic programming focuses on writing skeleton algorithms in terms of types that will be specified when the algorithm is actually used, thus allowing some leniency to programmers who wish to avoid strict strong typing rules. It can be a very powerful paradigm if well-implemented.  

*   **Imperative**  
Imperative languages allow programmers to give the computer ordered lists of instructions without necessarily having to explicitly state the task. It can be thought of being the opposite of declarative programming.  

*   **Structured**  
Structured programming languages aim to provide some form of noteworthy structure to a language, such as intuitive control over the order in which statements are executed (if X then do Y otherwise do Z, do X while Y is Z). Such languages generally deprecate "jumps", such as those provided by the goto statement in C and C++.  

*   **Procedural**  
Although it is sometimes used as a synonym for imperative programming, a procedural programming language can also refer to an imperative structured programming language which supports the concept of procedures and subroutines (also known as functions in C or C++).  

*   **Object-Oriented**  
Object-Oriented programming (sometimes abbreviated to OOP) is a subset of structured programming which expresses programs in the terms of "objects", which are meant to model objects in the real world. Such a paradigm allows code to be reused in remarkable ways and is meant to be easy to understand.  

###   Standardization  
Does a language have a formal standard? This can be very important to ensure that programs written to work with one compiler/interpreter will work with another. Some languages are standardized by the American National Standards Institute (ANSI), some are standardized by the International Organization for Standardization (ISO), and some have an informal but de-facto standard not maintained by any standards organization.  


# Repository Structure


```bash

                Repo/
                |
                |------- README.md
                |
                |------- LICENSE
                |
                |------- CONTRIBUTING.md
                |
                |------- CODE_OF_CONDUCT.md
                |
                |------- NOTICE.md
                |
                |
                |------- configs/
                |        |----- anyfile.json
                |
                |
                |
                |------- docs/
                |        |----- Index
                |        |----- Overview
                |        |----- API
                |        |----- Code Structure
                |        |----- Installation
                |        |----- Configuration
                |        |----- References
                |        |----- Future
                |        
                |
                |
                |------- src/
                         |  
                         |-----project/
                         |     |--__init__.py 
                         |     |--settings.py
                         |     |--urls.py
                         |     └--wsgi.py
                         |
                         |-----app1/  
                         |  
                         |  
                         |  
                         |-----app2-RESTful/  
                         |  
                         |  
                         |  
                         |-----manage.py  
                         |  
                         |  
                         |  
                         └-----db.sqlite3  
```                         

- [Django - Code of Conduct](https://www.djangoproject.com/conduct/)
- [Other - Code of Conduct](https://www.contributor-covenant.org/)

# History

## OS
- https://en.wikipedia.org/wiki/Timeline_of_operating_systems


# [Open Source Guide](https://opensource.guide/)


# Software Licensing

## Intro
- https://opensource.org/licenses/alphabetical
- http://www.gnu.org/licenses/
- https://opensource.org/licenses

## [Apache-2.0](https://opensource.org/licenses/Apache-2.0)
TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
- free, reproduce, sublicense, re-distribute in any form
- Redistribution
    - provide copy of license
    - mention you changed this file/code
    - retain copy of source code
- can be monitized   
- <a href="https://tldrlegal.com/license/apache-license-2.0-(apache-2.0)"> Summary</a>


## [MIT](https://opensource.org/licenses/MIT)
Permission is hereby granted, `free of charge`, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software `without restriction`, including without limitation the `rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies` of the Software, and to permit persons to whom the Software is furnished to do so.

- <a href="https://tldrlegal.com/license/mit-license"> Summary</a>

## [BSD-2-Clause](https://opensource.org/licenses/BSD-2-Clause)
Redistribution and use in source and binary forms, `with or without modification, are permitted provided` that the following conditions are met:

    1. Redistributions of source code must `retain the above copyright notice`, this list of conditions and the following disclaimer.

    2. Redistributions in binary form `must reproduce the above copyright notice`, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

- also known as `Simplified BSD` or `FreeBSD`
- can be monitized
- <a href="https://tldrlegal.com/license/bsd-2-clause-license-(freebsd)"> Summary</a>

## [BSD-3-Clause](https://opensource.org/licenses/BSD-3-Clause)
Redistribution and use in source and binary forms, `with or without modification, are permitted` provided that the following conditions are met:

    1. Redistributions of source code must `retain the above copyright notice`, this list of conditions and the following disclaimer.

    2. Redistributions in binary form must `reproduce the above copyright notice`, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

    3. Neither the `name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived` from this software without specific prior written permission.

- also known as `Modified BSD` or `New BSD`
- can be monitized
- <a href="https://tldrlegal.com/license/bsd-3-clause-license-(revised)"> Summary</a>

## [GPL-2.0](https://opensource.org/licenses/GPL-2.0)

- everyone is `permitted to copy and distribute verbatim copies
of this LICENSE document, but changing it is not allowed`

- can use, modify, redistribute

- original licensor can relicense to GPL-3.0
- also used as `GPL version 2 or any later version`
    - gives option to follow the terms and conditions of any later version
        - so, any other licensors can follow the the term & conditions of `GPL-3.0`
- can be monitized       
- modified versions of code/software be marked as changed with the date of the change
- any patent must be licensed for everyone's free use or not licensed at all
- <a href="https://tldrlegal.com/license/gnu-general-public-license-v2"> Summary</a>


## [GPL-3.0](https://opensource.org/licenses/GPL-3.0)
- everyone is `permitted to copy and distribute verbatim copies of this LICENSE document, but changing it is not allowed`

- can use, modify, redistribute
- else, similar to `GPL-2.0` but re-phrased
- <a href="https://tldrlegal.com/license/gnu-general-public-license-v3-(gpl-3)"> Summary</a>

## [AGPL-3.0](https://opensource.org/licenses/AGPL-3.0)

- everyone is `permitted to copy and distribute verbatim copies of this LICENSE document, but changing it is not allowed`

- built for network software
-  can distribute modified versions if you keep track of the changes and the date you made them
- source code must be distributed along with web service publication
- the AGPL is the GPL of the web
- http://www.gnu.org/licenses/agpl.html
- <a href="https://tldrlegal.com/license/gnu-affero-general-public-license-v3-(agpl-3.0)">Summary</a>




# Software Security

## Obfuscation
The process of protecting the protable executable files (EXE, DLL) from getting decompiled into the original source code is called Obfuscation.

### Obfuscation Tools
- ConfuserEx: https://yck1509.github.io/ConfuserEx/ (EXE, DLLs)
    - ConfuserEx Decoder: https://github.com/cawk/ConfuserEx-Unpacker
- dotfuscators: https://www.preemptive.com/products/dotfuscator/overview
- https://translate.google.it/translate?hl=it?sl=it&tl=en&u=https%3A//gianmarcocastagna.blogspot.it/


## Protect Code
- https://stackoverflow.com/questions/805461/how-to-protect-dlls
- https://stackoverflow.com/questions/109997/how-do-you-protect-your-software-from-illegal-distribution
- https://stackoverflow.com/questions/506282/protect-net-code-from-reverse-engineering
- https://www.codeproject.com/Articles/1139773/Protect-Your-Source-Code-from-Decompiling-or-Rever
- https://stackoverflow.com/questions/7849620/what-is-the-best-way-to-protect-sensitive-data-in-the-code


### Protect .Net Code
- https://stackoverflow.com/questions/7669684/encrypt-app-config-file-automatically-during-build-process


## Decompile Tools

- https://stackoverflow.com/questions/130058/how-are-serial-generators-cracks-developed

### DLLs
- dumpbin (c/c+)
- ILSpy
- dotPeek: https://www.jetbrains.com/decompiler/
- ReSharper

### Python
- [uncompyle6](https://pypi.org/project/uncompyle6/) (.pyc/.pyo to .py)
    - A native Python cross-version decompiler and fragment decompiler. The successor to decompyle, uncompyle, and uncompyle2.
- [pyinstallerextractor](https://sourceforge.net/projects/pyinstallerextractor/) (.exe to .py)


### PL/SQL
- [UnwrapIt](https://www.codecrete.net/UnwrapIt/)

## Encryption

### [Symmetric Key Encryption](https://en.wikipedia.org/wiki/Symmetric-key_algorithm)
- Intro
    - use the same cryptographic keys for both encryption of plaintext and decryption of ciphertext
    - The keys may be identical or there may be a simple transformation to go between the two keys
    - Insecure
    
#### [DES (Data Encryption Standard)](https://en.wikipedia.org/wiki/Data_Encryption_Standard)
- Intro
    - Insecure 
        - mainly due to the 56-bit key size being too small
        - Once hacked in 22hrs

#### [AES (Advanced Encryption Standard)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)
- Intro
    - a subset of Rijndael
    - superseded DES
    - uses block cipher
        - block cipher is a method of encrypting text (to produce ciphertext)
        - a cryptographic key and algorithm are applied to a block of data (for example, 64 contiguous bits) at once as a group rather than to one bit at a time
- Design Principle        
    - [substitution–permutation network](https://en.wikipedia.org/wiki/Substitution%E2%80%93permutation_network)
        - a combination of both substitution and permutation are applied to the plain text
    - fixed block size of 128 bits, and a key size of 128, 192, or 256 bits
- Variaties
    - MARS
    - RC6
    - Rijndael
    - Serpent
    - Twofish
    


### [Asymmetric Encryption (Private/Public Key)](https://en.wikipedia.org/wiki/Public-key_cryptography)
- Intro
    - pair of keys made up of long random strings
    - public key: known to every one
    - private key: known to owner only
- Functions
    - Authentication
        - public key verifies that message received is sent by paired private key holder only 
    - Encryption
        - only paired private key can decrypt the message encrypted by the public key

#### [Deffie-Hellman Key Exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange)
- http://www.omnisecu.com/security/public-key-infrastructure/asymmetric-encryption-algorithms.php
- Intro
    

#### [RSA (Rivest–Shamir–Adleman)](https://en.wikipedia.org/wiki/RSA_(cryptosystem))


## Misc

### .Net DLL vs C++ DLL
- https://stackoverflow.com/questions/10634743/net-dll-vs-c-dll

### 32 bit vs 64 bit DLL
- https://stackoverflow.com/questions/495244/how-can-i-test-a-windows-dll-file-to-determine-if-it-is-32-bit-or-64-bit

