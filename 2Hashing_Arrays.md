# Arrays & Sorting Patterns - Striver A2Z DSA Sheet

A quick revision guide to recognize the underlying pattern before solving an Array problem.

---

# 1. Basic Traversal Pattern (Single Pass)

## 💡 Idea

Traverse the array once while maintaining the required information.

### Problems

* Largest Element
* Second Largest Element
* Check if Array is Sorted
* Linear Search
* Maximum Consecutive Ones
* Leaders in an Array
* Stock Buy and Sell

### General Approach

* Traverse the array once.
* Maintain answer variables.
* Update them based on the current element.
* No extra data structure required.

**Time Complexity:** `O(n)`

---

# 2. In-place Modification Pattern (Two Pointer / Write Pointer)

## 💡 Idea

Maintain a pointer where the next valid element should be placed.

### Problems

* Remove Duplicates from Sorted Array
* Move Zeroes
* Rearrange Array by Sign (Optimized)

### General Approach

* One pointer scans.
* One pointer writes.
* Swap or copy elements whenever necessary.

**Time Complexity:** `O(n)`

---

# 3. Rotation Pattern

## 💡 Idea

Rotate the array efficiently without unnecessary shifts.

### Problems

* Left Rotate by One
* Left Rotate by K Places

### General Approach

### Method 1

* Extra Array

### Method 2 (Optimal)

Reverse Algorithm

1. Reverse first part
2. Reverse second part
3. Reverse entire array

**Time Complexity:** `O(n)`

---

# 4. Sorting Pattern

## 💡 Idea

Sort the array using different strategies.

### Problems

* Selection Sort
* Bubble Sort
* Insertion Sort
* Recursive Bubble Sort
* Recursive Insertion Sort
* Merge Sort
* Quick Sort

### General Approach

### Selection Sort

* Find minimum
* Swap

### Bubble Sort

* Push maximum to the end after each pass

### Insertion Sort

* Insert current element into the sorted left portion

### Merge Sort

* Divide
* Merge sorted halves

### Quick Sort

* Partition around pivot
* Recursively solve left and right halves

---

# 5. Binary Search on Sorted Property

## 💡 Idea

Use Binary Search on sorted arrays.

### Problems

*(No direct problems from this section.)*

---

# 6. Prefix Sum Pattern

## 💡 Idea

Maintain cumulative sums to answer range queries efficiently.

### Problems

* Longest Subarray Sum K
* Count Subarrays Sum K
* Largest Subarray Sum 0

### General Approach

Maintain

* Prefix Sum
* HashMap<PrefixSum, Index/Count>

Observation

* `prefix - previousPrefix = K`
* `prefix == previousPrefix` (depending on problem)

---

# 7. Sliding Window Pattern

## 💡 Idea

Maintain a valid window using two pointers.

### Problems

* Longest Subarray Sum K (Positive Numbers)

### General Approach

Maintain

* Left Pointer
* Right Pointer
* Current Sum

Operations

* Expand window
* Shrink when invalid
* Track maximum valid window

---

# 8. Hashing Pattern

## 💡 Idea

Store frequency or presence for constant-time lookup.

### Problems

* Union of Two Sorted Arrays
* Find Missing Number
* Number Appears Once
* Majority Element
* Majority Element II
* Longest Consecutive Sequence
* Repeating and Missing Number
* Count XOR K

### General Approach

Use

* HashMap
* HashSet

Perform lookups in `O(1)`.

---

# 9. XOR Pattern

## 💡 Idea

Exploit XOR properties.

### Problems

* Number Appears Once
* Find Missing Number (Alternative)
* Count XOR K

### General Approach

Properties

```text
a ^ a = 0
a ^ 0 = a
```

Convert the problem into XOR operations.

---

# 10. Mathematical Formula Pattern

## 💡 Idea

Derive the answer mathematically.

### Problems

* Pascal Triangle
* Find Missing Number
* Repeating and Missing Number

### General Approach

Use

* Sum Formula
* Square Sum Formula
* nCr
* Mathematical Derivation

Avoid extra space whenever possible.

---

# 11. Dutch National Flag Pattern

## 💡 Idea

Partition the array into three regions.

### Problems

* Sort 0s, 1s and 2s

### General Approach

Maintain

```text
low
mid
high
```

Regions

* 0 → Left
* 1 → Middle
* 2 → Right

---

# 12. Moore Voting Pattern

## 💡 Idea

Find majority element(s) in linear time.

### Problems

* Majority Element I
* Majority Element II

### General Approach

Phase 1

* Find candidate(s)

Phase 2

* Verify frequency

---

# 13. Kadane Pattern

## 💡 Idea

Maintain the best subarray ending at each index.

### Problems

* Maximum Subarray Sum
* Print Maximum Subarray

### General Approach

Maintain

```text
currentSum
maxSum
```

Whenever

```text
currentSum < 0
```

Reset

```text
currentSum = 0
```

Track indices if printing the subarray.

---

# 14. Greedy Pattern

## 💡 Idea

Make the best local choice while scanning.

### Problems

* Stock Buy and Sell
* Leaders in Array

### General Approach

Maintain the best answer seen so far.

Update greedily while traversing.

---

# 15. Matrix Traversal Pattern

## 💡 Idea

Traverse matrices carefully while respecting row/column boundaries.

### Problems

* Spiral Matrix
* Rotate Matrix
* Set Matrix Zeroes

### General Approach

Common Techniques

* Boundary Traversal
* Matrix Transpose
* Reverse Rows
* Marker Row/Column

---

# 16. Permutation Pattern

## 💡 Idea

Generate the next lexicographical arrangement.

### Problems

* Next Permutation

### General Approach

1. Find breakpoint.
2. Find next greater element.
3. Swap.
4. Reverse suffix.

---

# 17. Sorting + Two Pointer Pattern

## 💡 Idea

Sort first, then solve using two pointers.

### Problems

* Two Sum
* 3 Sum
* 4 Sum

### General Approach

1. Sort array.
2. Fix one/two elements.
3. Use two pointers.
4. Skip duplicates.

---

# 18. Merge Intervals Pattern

## 💡 Idea

Merge overlapping intervals after sorting.

### Problems

* Merge Overlapping Intervals

### General Approach

1. Sort intervals by start time.
2. If overlap → Merge.
3. Else → Add new interval.

---

# 19. Merge Sorted Arrays Pattern

## 💡 Idea

Merge without using extra space.

### Problems

* Merge Two Sorted Arrays Without Extra Space

### General Approach

Methods

* Gap Method (Shell Sort Idea)
* Swap & Sort
* Three Pointer (Extra Space Version)

---

# 20. Divide & Conquer Counting Pattern

## 💡 Idea

Count while merging.

### Problems

* Count Inversions
* Reverse Pairs

### General Approach

Use Modified Merge Sort.

During merge

* Count valid pairs.
* Merge sorted halves.

---

# 21. Prefix + HashMap Counting Pattern

## 💡 Idea

Maintain prefix information along with occurrence counts.

### Problems

* Count Subarrays Sum K
* Count Subarrays XOR K
* Largest Subarray Sum 0

### General Approach

Maintain

* Running Prefix
* HashMap storing previous prefixes

Use the relationship between

* Current Prefix
* Required Prefix

---

# 22. Simulation Pattern

## 💡 Idea

Implement exactly what the problem statement describes.

### Problems

* Next Permutation
* Pascal Triangle
* Spiral Matrix

### General Approach

Carefully simulate every operation while handling indices and boundary conditions.

---

# 📌 Final Revision Map

| Pattern                     | Problems                                                                         |
| --------------------------- | -------------------------------------------------------------------------------- |
| Basic Traversal             | Largest, Second Largest, Sorted Check, Linear Search, Leaders, Stock             |
| Two Pointer (Write Pointer) | Remove Duplicates, Move Zeroes, Rearrange by Sign                                |
| Rotation                    | Left Rotate 1, Left Rotate K                                                     |
| Sorting                     | Selection, Bubble, Insertion, Merge, Quick                                       |
| Sliding Window              | Longest Sum K (Positive)                                                         |
| Prefix Sum + HashMap        | Longest Sum K, Count Sum K, Largest Sum 0                                        |
| Hashing                     | Missing Number, Single Number, Majority, Consecutive Sequence, Repeating-Missing |
| XOR                         | Single Number, Missing Number, XOR K                                             |
| Mathematical Formula        | Pascal Triangle, Missing Number, Repeating-Missing                               |
| Dutch National Flag         | Sort 0s, 1s and 2s                                                               |
| Moore Voting                | Majority I, Majority II                                                          |
| Kadane                      | Maximum Subarray, Print Maximum Subarray                                         |
| Matrix Traversal            | Set Matrix Zeroes, Rotate Matrix, Spiral Matrix                                  |
| Sorting + Two Pointers      | Two Sum, 3 Sum, 4 Sum                                                            |
| Merge Intervals             | Merge Overlapping Intervals                                                      |
| Merge Sorted Arrays         | Merge Without Extra Space                                                        |
| Divide & Conquer            | Merge Sort, Count Inversions, Reverse Pairs                                      |
| Simulation                  | Next Permutation, Pascal Triangle, Spiral Matrix                                 |

---

# 🚀 Master Patterns to Remember

If you can recognize these patterns, almost every Array interview question becomes much easier.

1. Basic Traversal
2. Two Pointer / Write Pointer
3. Rotation
4. Sorting
5. Prefix Sum
6. Sliding Window
7. Hashing
8. XOR
9. Mathematical Formula
10. Dutch National Flag
11. Moore Voting
12. Kadane
13. Greedy
14. Matrix Traversal
15. Permutation
16. Sorting + Two Pointers
17. Merge Intervals
18. Merge Sorted Arrays
19. Divide & Conquer
20. Simulation
