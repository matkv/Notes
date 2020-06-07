# Compiler

A computer program which translates computer code written in one programming language (source language) into another language (target language) - for example translating source code from a **high level programming language** into a **lower level** language (assembly, machine code).

A compiler usually performs the following operations:

* preprocessing
* semantic analysis (datatype compatibility..)
* parsing
* code optimization
* code generation
* syntax analysis (brackets...)

## Types of compilers

* **native compiler** - generates code for the same platform it runs on
* **cross compiler** - generates code for a different plattform than the one it runs on
* **single pass compiler** - only one pass while generating the code, fast, little optimization
* **multi pass compiler** - more optimization and gathering information about declarations
* **source to source** - high level language as the input, high level language as the output
* **Just-in-time compiler** - compilation during runtime. A JIT compiler generally runs inside an intepreter
* **assembler** - compiles human readable assembly language to machine code