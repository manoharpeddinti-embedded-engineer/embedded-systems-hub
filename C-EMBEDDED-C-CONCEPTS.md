# C / Embedded-C Concepts to Master

A concepts-first learning guide for embedded and firmware interviews. This is **not** a question bank: use it to build the knowledge needed before you practise programming problems.

## Priority order

### Must know first

1. [C fundamentals](#1-c-fundamentals)
2. [Pointers](#2-pointers)
3. [Arrays and strings](#3-arrays-and-strings)
4. [`const`, `volatile`, and `static`](#4-const-volatile-and-static)
5. [Memory layout and dynamic memory](#5-memory-layout-and-dynamic-memory)
6. [Structures, unions, alignment, and padding](#6-structures-unions-alignment-and-padding)
7. [Bit manipulation](#7-bit-manipulation)
8. [Functions and callbacks](#8-functions-and-callbacks)
9. [Storage, scope, linkage, and the preprocessor](#9-storage-scope-linkage-and-the-preprocessor)
10. [Memory-mapped register programming](#10-memory-mapped-register-programming)

### Next level

11. [Endianness and integer details](#11-endianness-and-integer-details)
12. [`sizeof` and declarations](#12-sizeof-and-declarations)
13. [Undefined and implementation-defined behavior](#13-undefined-and-implementation-defined-behavior)
14. [Compiler, linker, and startup](#14-compiler-linker-and-startup)
15. [Optimization and compiler behavior](#15-optimization-and-compiler-behavior)
16. [Interrupt-safe C](#16-interrupt-safe-c)
17. [Reentrancy and thread safety](#17-reentrancy-and-thread-safety)
18. [Defensive C and coding standards](#18-defensive-c-and-coding-standards)

---

## 1. C fundamentals

Understand the built-in types (`char`, `short`, `int`, `long`), signed versus unsigned values, fixed-width integer types such as `uint8_t` and `uint32_t`, ranges, casts, conversion rules, integer promotions, overflow/underflow, operators, precedence, control flow, functions, declarations versus definitions, scope, and lifetime.

For firmware, know why fixed-width types matter when code talks to registers, protocols, and hardware-defined data formats.

## 2. Pointers

Pointers are a core firmware-interview topic. Understand addresses and dereferencing, pointer arithmetic, arrays and pointers, pointers to pointers, `void *`, NULL/dangling/wild pointers, function pointers, callbacks, arrays of pointers, pointers to arrays, and multidimensional arrays.

Be able to read these immediately:

```c
const int *p;      // pointer to const int
int *const p;      // const pointer to int
const int *const p; // const pointer to const int
```

## 3. Arrays and strings

Learn 1D/2D arrays, initialisation, indexing, array-to-pointer decay, passing arrays to functions, multidimensional-array layout, and `sizeof(array)` versus `sizeof(pointer)`.

For strings, understand null termination, character arrays versus string literals, buffer sizes, and the purpose and risks of `strlen`, `strcpy`, `strncpy`, `strcmp`, `memcpy`, `memmove`, `memset`, and `strcat`.

Know why the following are not equivalent when modification is attempted:

```c
char a[] = "hello";
char *p = "hello";
```

## 4. `const`, `volatile`, and `static`

These keywords are especially important in Embedded C.

- `volatile`: explains that a value may change outside ordinary program flow, for example a memory-mapped register or a variable shared with an ISR. It does **not** make access atomic and does **not** replace synchronization.
- `const`: protects data through the type system; understand const objects, pointers to const, const pointers, and const parameters.
- `static`: understand static local lifetime, file-local globals/functions, visibility, and internal linkage.

## 5. Memory layout and dynamic memory

Know the usual C-program regions: code/text, read-only data, `.data`, `.bss`, heap, and stack. Be able to reason about where functions, globals, static data, local variables, string literals, and dynamically allocated objects commonly live.

Also understand stack frames, recursion, stack overflow, and `malloc`, `calloc`, `realloc`, and `free`. Know memory leaks, dangling pointers, double frees, use-after-free, fragmentation, heap exhaustion, and NULL checks.

For embedded systems, explain why dynamic allocation is often restricted: determinism, fragmentation, limited RAM, and failure handling.

## 6. Structures, unions, alignment, and padding

Understand structure declaration, initialisation, member access (`.` and `->`), nested structures, arrays of structures, passing structures, and `sizeof(struct)`.

Know the difference between a struct and a union, how union storage is shared, and why type-punning has portability concerns. Learn natural alignment, padding, packed structures, unaligned access, and why blindly applying packing can create problems.

## 7. Bit manipulation

Be fluent with `&`, `|`, `^`, `~`, `<<`, and `>>`. Build confidence with masks: setting, clearing, toggling, and checking bits; updating a field without disturbing neighbouring bits; extracting bit fields; counting set bits; checking powers of two; and byte/nibble manipulation.

This is essential for registers, status flags, protocol fields, and peripheral configuration.

## 8. Functions and callbacks

Know call by value, using pointers to update caller-owned data, prototypes, return values, arrays/structures/pointers as parameters, recursion, inline functions, function pointers, callbacks, callback tables, and state-machine dispatch.

Function-pointer callbacks appear frequently in drivers, event systems, and hardware abstraction layers.

## 9. Storage, scope, linkage, and the preprocessor

Understand `auto`, `static`, `extern`, and `register`; local/global variables; block and file scope; internal/external linkage; storage duration; definitions versus declarations; and sharing declarations across `.c` files through headers.

For the preprocessor, know `#define`, function-like macros, macro parentheses and side effects, `#ifdef`, `#ifndef`, `#if`, header guards, `#include`, predefined macros, stringification (`#`), and token pasting (`##`).

## 10. Memory-mapped register programming

This is where generic C becomes Embedded C. Understand register addresses, pointer casts, `volatile`, masks, read-modify-write behavior, register fields, and read-only/write-only registers.

For example, be able to explain why firmware may use:

```c
volatile uint32_t *reg;
```

## 11. Endianness and integer details

Know little-endian and big-endian representation, byte swapping, network byte order, reading memory dumps, and the impact of byte order on protocols and registers.

Also study signed/unsigned comparison, truncation, sign extension, fixed-width types from `stdint.h`, `size_t`, integer literals, casts, and the risks of shifting signed values.

## 12. `sizeof` and declarations

Understand `sizeof` for arrays, pointers, structs, unions, strings, types, expressions, and function parameters. In particular, know why an array passed to a function no longer retains its original array size for `sizeof`.

## 13. Undefined and implementation-defined behavior

Learn the difference among undefined, implementation-defined, and unspecified behavior. Common risk areas include uninitialised variables, signed overflow, out-of-bounds access, invalid shifts, invalid pointers, use-after-free, writing to string literals, evaluation-order pitfalls, and strict aliasing.

## 14. Compiler, linker, and startup

Understand the path from source code to firmware:

```text
Source → Preprocessor → Compiler → Assembler → Object file → Linker → Firmware
```

Know `.c` versus `.h`, object files, symbol resolution, compiler errors versus linker errors, static libraries, linker scripts at a basic level, map files, and the `.text`, `.data`, and `.bss` sections.

For stronger embedded roles, learn startup code and how `.data` and `.bss` are prepared before `main()`.

## 15. Optimization and compiler behavior

Know what compiler optimization changes, why `-O0` and optimized builds can behave differently, dead-code elimination, register allocation, inlining, and why some hardware/shared-state access needs `volatile`.

## 16. Interrupt-safe C

Understand ISR-shared variables, atomicity, race conditions, reentrancy, critical sections, and why blocking work is unsuitable inside an ISR. Remember: `volatile` does not make compound operations atomic.

## 17. Reentrancy and thread safety

Know the difference between reentrant and non-reentrant functions, the risks of static/global state and shared buffers, and how race conditions affect main-loop, ISR, and RTOS-task code.

## 18. Defensive C and coding standards

For safety-oriented firmware roles, learn the purpose of MISRA C, static analysis, compiler warnings, explicit initialisation, bounds checks, and defensive-programming practices.

## Further reading

- [Barr Group Embedded C Coding Standard](https://barrgroup.com/sites/default/files/barr_c_coding_standard_2018.pdf)
- [Barr Group: `volatile` keyword](https://info.barrgroup.com/embedded-systems/how-to/c-volatile-keyword)
- [Embedded Artistry: Embedded C interview-question breakdown](https://embeddedartistry.com/blog/2017/06/05/interview-question-breakdown-bad-c-analysis/)

## What comes next

After these concepts are in place, move to the hub’s future **C programming practice** and **Embedded-C interview questions** sections. Keep theory and question practice separate: understand the rule first, then practise applying it.
