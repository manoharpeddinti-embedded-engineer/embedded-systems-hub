# Hands-on C / Embedded-C Exercises

Write, compile, test, and explain your solution. These exercises test implementation and debugging ability—not just definitions.

For theory and explanation prompts, see [150 C / Embedded-C Interview Questions](C-EMBEDDED-C-INTERVIEW-QUESTIONS.md).

## 1. Bit manipulation and registers — 1–15

1. Write a function to set the nth bit of a 32-bit value.
2. Write functions to set, clear, toggle, and read a selected bit.
3. Set bits 4–7 of a register without changing other bits.
4. Replace bits `[11:8]` with a supplied 4-bit value.
5. Count set bits in a 32-bit integer.
6. Reverse all bits in a 32-bit integer.
7. Swap upper and lower nibbles of an 8-bit value.
8. Swap odd and even bits of a 32-bit integer.
9. Test whether a number is a power of two without division or loops.
10. Convert `0x12345678` to `0x78563412`.
11. Implement `SET_BIT`, `CLEAR_BIT`, `TOGGLE_BIT`, and `CHECK_BIT` macros safely.
12. Access a memory-mapped register at `0x40001000` as a volatile 32-bit register.
13. Update a register field using mask, shift, and value while preserving unrelated bits.
14. Extract the third byte from a 32-bit integer.
15. Find the position of the first set bit in an unsigned integer.

## 2. Pointers and memory — 16–25

16. Implement `memcpy()`.
17. Implement overlap-safe `memmove()`.
18. Implement `memset()`.
19. Swap two integers through pointers.
20. Dynamically allocate an integer array, return it to the caller, and handle allocation failure.
21. Safely read a 32-bit little-endian value from a buffer without reading beyond its bounds.
22. Write a function that receives a pointer-to-pointer and changes the caller’s pointer.
23. Demonstrate the difference between pointer-to-array and array-of-pointers.
24. Implement a generic swap using `void *`.
25. Given an array-element pointer, move to the next element; explain the difference for `uint8_t *` and `uint32_t *`.

## 3. Strings — 26–35

26. Implement `strlen()` without library functions.
27. Implement `strcpy()` and document your destination-size assumption.
28. Implement `strcmp()`.
29. Reverse a string in place.
30. Check whether a string is a palindrome.
31. Remove duplicate characters from a string.
32. Find the first non-repeating character.
33. Count frequency of every character.
34. Reverse words in a sentence while preserving each word’s character order.
35. Copy at most `destination_size - 1` characters and always null-terminate when destination size is nonzero.

## 4. Arrays — 36–45

36. Find the largest and second-largest distinct values in one traversal.
37. Find the missing value from `1` to `N` when exactly one is absent.
38. Remove duplicates from a sorted array in place.
39. Rotate an array right by `K` without allocating an array proportional to `N`.
40. Merge two sorted arrays.
41. Find the intersection of two arrays.
42. Implement binary search.
43. Move all zeros to the end while preserving nonzero order.
44. Find maximum contiguous subarray sum.
45. Find the single number when every other number appears twice, using O(1) extra memory.

## 5. Embedded-style implementation — 46–50

46. Implement a fixed-size ring buffer: `init()`, `push()`, `pop()`, `isFull()`, and `isEmpty()`.
47. Implement an `enum` + `switch` finite-state machine for `IDLE → START → RUNNING → ERROR`, with `RUNNING → DONE`.
48. Implement a function-pointer callback system where a driver invokes a registered function on an event.
49. Design UART receive handling where an ISR pushes bytes into a ring buffer and the main loop processes them. Explain shared state, `volatile`, atomicity, and ISR length.
50. Fix this polling code for a hardware status register that changes asynchronously:

```c
uint32_t *status = (uint32_t *)0x40000000;

while ((*status & 0x01) == 0)
{
}

printf("Ready\n");
```

State what is wrong, correct the declaration, and explain why.

## 6. Predict / debug this code — 51–55

51. Diagnose and redesign the API appropriately:

```c
int *getValue(void)
{
    int x = 10;
    return &x;
}
```

52. Rewrite `update()` so the caller receives the allocated pointer and allocation failure is handled:

```c
void update(int *p)
{
    p = malloc(sizeof(int));
    *p = 100;
}
```

53. Explain whether this is valid and why:

```c
char *p = "hello";
p[0] = 'H';
```

54. Identify every issue in this code:

```c
int *p = malloc(10 * sizeof(*p));
free(p);
p[0] = 20;
free(p);
```

55. Diagnose ISR-shared state and explain why `volatile` does not solve every synchronization issue:

```c
int flag = 0;

void ISR(void)
{
    flag = 1;
}

int main(void)
{
    while (flag == 0)
    {
    }
    process();
}
```

## How to use this bank

For every practical task:

1. Write the code without copying a solution.
2. Define assumptions, input constraints, and error behavior.
3. Compile with strict warnings enabled.
4. Test normal, boundary, and invalid inputs.
5. Explain time/space cost and embedded trade-offs such as RAM, atomicity, and determinism.

## Suggested expansion

This first practical set has 55 detailed tasks. Future additions can grow it to the planned 100 practical prompts by adding more predict-output, debugging, unit-test, and board-oriented scenarios—without duplicating the 150 theory questions.
