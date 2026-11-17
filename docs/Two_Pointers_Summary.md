# Introduction to Two Pointers - Summary

## Table of Contents
- [Overview](#overview)
- [What is a Pointer?](#what-is-a-pointer)
- [Types of Two Pointer Techniques](#types-of-two-pointer-techniques)
  - [1. Opposite Direction](#1-opposite-direction-converging-pointers)
  - [2. Same Direction](#2-same-direction-parallel-pointers)
  - [3. Fixed Offset](#3-fixed-offset-pointers)
- [When Sorting Is Required](#when-sorting-is-required)
- [When to Use Two Pointers](#when-to-use-two-pointers)
- [When Not to Use Two Pointers](#when-not-to-use-two-pointers)
- [Complexity Summary](#complexity-summary)

## Overview

Two Pointers is a technique that uses two indices to traverse a linear data structure such as an array, string, or linked list.

Key benefit:
- Often reduces brute-force O(n²) solutions to O(n)
- Some problems require sorting first, leading to O(n log n)
- Usually uses O(1) extra space

## What is a Pointer?

A pointer typically represents an index or position within a data structure.

Common uses:
- Left and right boundaries
- Read and write positions
- Two arrays being merged
- Fast and slow traversal speeds

## Types of Two Pointer Techniques

### 1. Opposite Direction (Converging Pointers)

One pointer starts from the beginning and the other from the end.

```java
int left = 0;
int right = nums.length - 1;

while (left < right) {
    int sum = nums[left] + nums[right];

    if (sum == target) {
        break;
    } else if (sum < target) {
        left++;
    } else {
        right--;
    }
}
```

Typical problems:
- Two Sum II (sorted array)
- Valid Palindrome
- Container With Most Water

Example: Palindrome Check

```java
boolean isPalindrome(String s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }

    return true;
}
```

Complexity:
- Time: O(n)
- Space: O(1)

---

### 2. Same Direction (Parallel Pointers)

Both pointers move forward but play different roles.

- Read pointer scans data
- Write pointer maintains valid region

Example: Remove Duplicates from Sorted Array

```java
int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;

    int write = 1;

    for (int read = 1; read < nums.length; read++) {
        if (nums[read] != nums[read - 1]) {
            nums[write++] = nums[read];
        }
    }

    return write;
}
```

Complexity:
- Time: O(n)
- Space: O(1)

#### Sliding Window

A specialized same-direction technique.

Used for:
- Longest substring without repeating characters
- Smallest subarray with target sum

#### Fast and Slow Pointers

Used for:
- Detecting cycles in linked lists
- Finding middle node

Example (Floyd Cycle Detection):

```java
ListNode slow = head;
ListNode fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow == fast) {
        return true;
    }
}

return false;
```

Complexity:
- Time: O(n)
- Space: O(1)

---

### 3. Fixed-Offset Pointers

One pointer advances first to create a fixed gap.

Classic example: Find Nth node from end.

```java
ListNode fast = head;
ListNode slow = head;

for (int i = 0; i < n; i++) {
    fast = fast.next;
}

while (fast != null) {
    fast = fast.next;
    slow = slow.next;
}

return slow;
```

Complexity:
- Time: O(n)
- Space: O(1)

## When Sorting Is Required

Sorting is required for pair-sum style problems where pointer movement depends on element ordering.

Examples:
- Two Sum II
- 3Sum

Complexity after sorting:
- Sorting: O(n log n)
- Two-pointer scan: O(n)
- Overall: O(n log n)

Sorting is NOT required for:
- Palindrome checks
- Sliding window problems
- Fast/slow pointers
- Read/write partition problems

## When to Use Two Pointers

Use when working with:
- Arrays
- Strings
- Linked Lists

Common scenarios:

1. Sorted array pair/triplet problems
2. In-place array modification
3. Palindrome checking
4. Merging sorted sequences
5. Sliding window problems with monotonic behavior

## When Not to Use Two Pointers

Avoid when:

- Sorting changes the required answer
- No monotonic relationship exists
- Need all arbitrary combinations
- Problem requires non-contiguous combinations

## Complexity Summary

| Pattern | Time | Space | Typical Examples |
|----------|------|--------|------------------|
| Opposite Direction | O(n) | O(1) | Two Sum II, Palindrome |
| Same Direction | O(n) | O(1) | Remove Duplicates, Move Zeroes |
| Sliding Window | O(n) | O(1) | Longest Substring |
| Fast & Slow | O(n) | O(1) | Cycle Detection |
| Fixed Offset | O(n) | O(1) | Nth Node From End |
| Sort + Two Pointers | O(n log n) | O(1) / O(log n) | 3Sum, Pair Sum |

## Key Interview Insight

When you see:
- Sorted arrays
- Palindromes
- In-place modifications
- Subarrays/substrings
- Linked list cycle detection

Always consider whether a Two Pointer solution can replace nested loops and reduce complexity from O(n²) to O(n).
