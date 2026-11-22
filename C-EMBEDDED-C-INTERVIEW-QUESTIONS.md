# 150 C / Embedded-C Interview Questions

These questions cover recurring concepts for embedded and firmware roles. They are high-value preparation prompts, **not** a guarantee of what a specific company will ask.

For hands-on implementation work, use [Hands-on C / Embedded-C Exercises](C-EMBEDDED-C-PRACTICAL-EXERCISES.md).

## 1. C fundamentals and data types — 1–10

1. What are the fundamental C data types, and what determines their actual sizes on a platform?
2. What is the difference among `signed`, `unsigned`, and plain integer types?
3. Why are `uint8_t`, `uint16_t`, and `uint32_t` common in embedded software?
4. What are integer promotions and the usual arithmetic conversions?
5. What happens when a negative signed integer is compared with an unsigned integer?
6. What is the difference between implicit conversion and explicit casting?
7. What happens when an oversized value is converted to an unsigned destination type?
8. Why can signed overflow be more dangerous than unsigned wraparound?
9. What is the difference among declaration, definition, and initialization?
10. Explain scope, storage duration, and linkage. Why are they distinct concepts?

## 2. Pointers — 11–30

11. What does a pointer variable store?
12. Explain the difference among `&p`, `p`, and `*p`.
13. What is pointer arithmetic, and why does `p + 1` depend on the pointed-to type?
14. Distinguish NULL, dangling, and uninitialized/wild pointers.
15. What is `void *`, and when is it useful?
16. Why can `void *` convert to/from object pointers in C, but not be portably dereferenced directly?
17. Explain `const int *p`, `int *const p`, and `const int *const p`.
18. What is a pointer to a pointer? Give a practical use case.
19. Explain the difference between `int *p[10]` and `int (*p)[10]`.
20. How do you pass a pointer when a function must modify the caller’s pointer?
21. What is a function pointer?
22. Declare a function pointer taking two `int` values and returning an `int`.
23. Where are function pointers useful in embedded systems?
24. How would you implement callbacks with function pointers?
25. What can happen after dereferencing a NULL pointer?
26. What can happen when returning the address of a local automatic variable?
27. What is pointer aliasing?
28. What alignment problems can pointer casts introduce?
29. Why might embedded code cast a hardware address integer to a pointer, and what portability risks arise?
30. How do you systematically read a complex pointer declaration?

## 3. Arrays and strings — 31–42

31. What is the difference between an array and a pointer?
32. When does an array expression decay into a pointer, and what are the exceptions?
33. Why can `sizeof(array)` and `sizeof(pointer)` differ?
34. What happens to an array parameter in a function declaration?
35. How are multidimensional arrays laid out in memory?
36. Explain the difference between `char a[] = "hello";` and `char *p = "hello";`.
37. Why must a C string end in `\0`?
38. Compare `strlen()` and `sizeof()` for a string array.
39. What are the risks of `strcpy()` and `strcat()`?
40. What is the difference between `memcpy()` and `memmove()`?
41. Why is overlapping source/destination memory a problem for `memcpy()`?
42. How would you reverse a string in place without another array?

## 4. `const`, `volatile`, `static`, and `extern` — 43–57

43. What does `const` mean in C?
44. Does `const` guarantee physically read-only memory?
45. Explain pointer-to-const versus const-pointer.
46. What does `volatile` tell the compiler?
47. Name three embedded situations where `volatile` may be required.
48. Why are memory-mapped hardware registers commonly `volatile`?
49. Why might an ISR-modified variable need `volatile`?
50. Does `volatile` make an operation atomic?
51. Does `volatile` make code thread-safe?
52. Can an object be both `const` and `volatile`? Give a hardware example.
53. Explain `volatile uint32_t * const reg`.
54. What happens to the lifetime of a static local variable?
55. What does `static` mean for a file-scope variable?
56. What does `static` mean for a function?
57. What does `extern` mean, and how do two `.c` files safely share a global variable?

## 5. Memory layout and dynamic memory — 58–70

58. Explain `.text`, read-only data, `.data`, `.bss`, heap, and stack.
59. Where does an initialized global typically live?
60. Where does an uninitialized global/static typically live?
61. Where does a string literal typically live?
62. What happens to automatic locals when a function returns?
63. What is a stack frame?
64. What causes stack overflow in an embedded system?
65. Explain `malloc()`, `calloc()`, `realloc()`, and `free()`.
66. Compare `malloc()` and `calloc()`.
67. What is a memory leak?
68. Explain use-after-free, double-free, and dangling pointers.
69. What is heap fragmentation?
70. Why do many safety-critical or constrained embedded systems restrict dynamic allocation after initialization?

## 6. Structures, unions, enums, and alignment — 71–82

71. What is structure padding, and why is it inserted?
72. What is data alignment?
73. Given `struct A { char a; int b; char c; };`, what information is needed before asserting its exact size?
74. How can member order reduce padding?
75. Compare a structure and a union.
76. How is union size determined?
77. Where can unions be useful in embedded programming?
78. What risks come with packed structures?
79. Why can unaligned access be problematic on some processors?
80. What is an `enum`, and when is it better than numeric macros?
81. What does `typedef` do? Does it create a fundamentally distinct C type?
82. What does `offsetof()` do, and where is it useful?

## 7. Bit manipulation — 83–97

83. How do you set the nth bit?
84. How do you clear the nth bit?
85. How do you toggle the nth bit?
86. How do you test whether the nth bit is set?
87. How would you count set bits in a 32-bit integer?
88. How do you test whether a nonzero unsigned value is a power of two efficiently?
89. Explain `x &= (x - 1);`.
90. How do you extract bits `[7:4]` from a register?
91. How do you update bits `[7:4]` without changing other bits?
92. How do you swap upper and lower nibbles of an 8-bit value?
93. How would you reverse bits in an 8-bit value?
94. How do you set multiple register bits with a mask?
95. What is risky about shifting by at least the width of the promoted operand?
96. Compare logical and arithmetic right shift; what does C guarantee for negative signed values?
97. Why are unsigned types usually better for bit manipulation?

## 8. Endianness and byte manipulation — 98–104

98. Explain little-endian and big-endian byte order.
99. How would you write a portable runtime endianness check?
100. Does endianness change an integer’s numeric value or its in-memory byte representation?
101. How do you byte-swap a 32-bit unsigned value?
102. How can you extract bytes from a `uint32_t` without relying on host endianness?
103. What is network byte order?
104. How do you safely reconstruct a 32-bit big-endian protocol value from four bytes?

## 9. Macros and preprocessor — 105–115

105. Compare a macro and a function.
106. What is wrong with `#define SQUARE(x) x*x`?
107. Why is `SQUARE(i++)` dangerous even if the macro is parenthesized?
108. Why should macro parameters and the full macro expression be parenthesized?
109. What is conditional compilation?
110. Explain `#if`, `#ifdef`, `#ifndef`, `#elif`, and `#endif`.
111. What problem do header guards solve?
112. Compare `#define` constants, `const` objects, and `enum` constants.
113. What do `#` and `##` do in the preprocessor?
114. What is a multi-statement macro, and why use `do { ... } while (0)`?
115. When is an `inline` function preferable to a function-like macro?

## 10. Functions, callbacks, and state machines — 116–124

116. Does C support pass-by-reference, or only pass-by-value?
117. What happens conceptually during a normal function call?
118. What are the benefits and risks of recursion in embedded systems?
119. Why is recursion prohibited in some embedded projects?
120. What is a callback function?
121. How would you design a function-pointer table for device events?
122. How can function pointers implement a state machine?
123. What is a reentrant function?
124. What makes a function non-reentrant?

## 11. Memory-mapped I/O and Embedded C — 125–134

125. What is memory-mapped I/O?
126. Why can’t peripheral registers always be handled like ordinary RAM?
127. Explain `volatile uint32_t * const GPIO_REG = (volatile uint32_t *)0x40000000u;`.
128. How do you set a GPIO control bit without intentionally changing other bits in a normal read/write register?
129. What is a read-modify-write operation?
130. Why can read-modify-write be unsafe for certain registers or concurrent execution contexts?
131. What are write-one-to-clear registers, and why can ordinary read-modify-write be wrong?
132. Why can missing `volatile` break polling of asynchronously changing status registers?
133. Why must the peripheral datasheet guide register manipulation?
134. What can happen if reserved register bits are modified?

## 12. Interrupts, concurrency, and atomicity — 135–142

135. How should a global flag written by an ISR and read by `main()` be declared, and why?
136. Why is `volatile` alone insufficient for read-modify-write shared with an ISR?
137. What is an atomic operation?
138. What is a race condition?
139. What is a critical section?
140. Why should ISRs be short?
141. Why are blocking operations inappropriate in an ISR?
142. How would you safely exchange data between an ISR and main-loop/task context?

## 13. Undefined behavior, compiler, and optimization — 143–150

143. What is undefined behavior? Give five examples.
144. Compare undefined, unspecified, and implementation-defined behavior.
145. Why is reading an uninitialized automatic variable serious?
146. Why can buggy code work at `-O0` and fail when optimized?
147. What can a compiler optimize when it proves a computation has no observable effect?
148. Explain preprocessing → compilation → assembly → linking.
149. Compare compiler, linker, and runtime errors; give an example of each.
150. A firmware image works in debug but fails in release. How would you investigate undefined behavior, missing `volatile`, races, timing, corruption, stack usage, warnings, and generated assembly?

## Related resources

- [C / Embedded-C Concepts to Master](C-EMBEDDED-C-CONCEPTS.md)
- [Hands-on C / Embedded-C Exercises](C-EMBEDDED-C-PRACTICAL-EXERCISES.md)
- [Barr Group Embedded C Coding Standard](https://barrgroup.com/sites/default/files/barr_c_coding_standard_2018.pdf)
- [Embedded Artistry: Embedded C interview-question breakdown](https://embeddedartistry.com/blog/2017/06/05/interview-question-breakdown-bad-c-analysis/)
