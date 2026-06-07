# Basic Recursion Pattern

## Recursion Template

For every recursion problem, answer these 3 questions:

1. What does my function represent? (State / Task)
2. What is my base case?
3. How do I reduce the problem size?

---

# 1. Print 1 to N

```java
class Solution {
    public void printNumbers(int n) {
        print(1, n);
    }

    private void print(int i, int n) {

        // All numbers have been printed
        if (i > n) return;

        System.out.println(i);

        // Ask recursion to print remaining numbers
        print(i + 1, n);
    }
}
```

### Interview Explanation

**State:**

* `i` = current number

**Task:**

* Print numbers from `i` to `n`

**Base Case:**

* When `i > n`, all numbers are printed.

**Smaller Problem:**

* After printing `i`, recursion prints `i+1` to `n`.

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 2. Print N to 1

```java
class Solution {
    public void printNumbers(int n) {
        print(n);
    }

    private void print(int n) {

        // No numbers left to print
        if (n < 1) return;

        System.out.println(n);

        // Print remaining numbers
        print(n - 1);
    }
}
```

### Interview Explanation

**State:**

* `n` = current number

**Task:**

* Print numbers from `n` to `1`

**Base Case:**

* When `n < 1`

**Smaller Problem:**

* After printing `n`, recursion prints `n-1` to `1`.

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 3. Sum of First N Numbers

```java
class Solution {

    public int NnumbersSum(int n) {

        // Sum of first 0 numbers is 0
        if (n == 0) return 0;

        // Current number + sum of smaller numbers
        return n + NnumbersSum(n - 1);
    }
}
```

### Interview Explanation

**State:**

* `n`

**Task:**

* Return sum of first `n` natural numbers

**Observation:**

```text
Sum(n) = n + Sum(n-1)
```

**Base Case:**

```text
Sum(0) = 0
```

**Smaller Problem:**

* Recursion calculates `Sum(n-1)`.

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 4. Factorial

```java
class Solution {

    public int factorial(int n) {

        // 0! and 1! are both 1
        if (n <= 1) return 1;

        // n! = n × (n-1)!
        return n * factorial(n - 1);
    }
}
```

### Interview Explanation

**State:**

* `n`

**Task:**

* Return `n!`

**Observation:**

```text
n! = n × (n-1)!
```

**Base Case:**

```text
0! = 1
1! = 1
```

**Smaller Problem:**

* Recursion computes `(n-1)!`

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 5. Fibonacci Number

```java
class Solution {

    public int fib(int n) {

        // Known answers
        if (n <= 1) return n;

        // nth Fibonacci = previous two Fibonacci numbers
        return fib(n - 1) + fib(n - 2);
    }
}
```

### Interview Explanation

**State:**

* `n`

**Task:**

* Return nth Fibonacci number

**Observation:**

```text
Fib(n) = Fib(n-1) + Fib(n-2)
```

**Base Cases:**

```text
Fib(0) = 0
Fib(1) = 1
```

**Smaller Problems:**

* Calculate `Fib(n-1)`
* Calculate `Fib(n-2)`

### Complexity

```text
TC = O(2^N)
SC = O(N)
```

### Why TC is O(2^N)?

Because each function call creates approximately two more calls:

```text
fib(n)
├── fib(n-1)
└── fib(n-2)
```

Many subproblems are recalculated repeatedly.

# Time Complexity of Recursive Fibonacci

The recursive approach for calculating Fibonacci numbers has a time complexity of **O(2ⁿ)**. This exponential growth happens because the algorithm repeatedly recalculates the same numbers.

---

# 1. The Intuitive Explanation

To find a Fibonacci number, the algorithm calls itself twice (to get the two previous numbers):

```text
F(n) = F(n-1) + F(n-2)
```

If you visualize this as an upside-down tree, the top node (for `F(n)`) branches into two nodes. Each of those branches into two more, and so on, until it reaches the base cases `F(1)` and `F(0)`.

### The Problem

The tree grows at an exponential rate of:

```text
2^n
```

### The Redundancy

To calculate `F(5)`, the function recalculates:

```text
F(3) twice
F(2) three times
```

As `n` gets larger, the number of duplicate calculations explodes, making this approach extremely slow for large inputs.

---

# 2. Solving with the Akra-Bazzi Method

While often used for divide-and-conquer algorithms, the Akra-Bazzi method can mathematically prove the complexity of Fibonacci recursion.

The recurrence relation for Fibonacci is:

```text
T(n) = T(n-1) + T(n-2) + c
```

To apply Akra-Bazzi, we use the general form:

```text
Σ(ai * bi^p) = 1
```

For Fibonacci:

```text
a1 = 1
b1 = 1

a2 = 1
b2 = 1
```

(using approximations for `T(n-1)` and `T(n-2)`).

Solving the equation for `p` yields the **Golden Ratio**:

```text
φ = (1 + √5) / 2
```

Numerically:

```text
φ ≈ 1.618
```

Since the constant work `c` is only a polynomial term, the dominant term determines the complexity.

Therefore:

```text
T(n) = O(φ^n)
```

or approximately:

```text
O(1.618^n)
```

Since:

```text
1.618^n < 2^n
```

it is commonly written as:

```text
O(2^n)
```

which is a simpler exponential upper bound.

---

# 3. Common Time Complexity of Non-Tail Recursion

A **non-tail recursive function** is one where the recursive call is **not the last operation executed**.

Example:

```java
return fib(n-1) + fib(n-2);
```

The addition still has to be performed after the recursive calls return, so this is non-tail recursion.

---

## Single Branch Recursion

Example:

```text
T(n) = T(n-1) + O(1)
```

This creates a straight-line call stack:

```text
n
|
n-1
|
n-2
|
...
```

Time Complexity:

```text
O(n)
```

---

## Multiple Branch Recursion

Example:

```text
T(n) = T(n-1) + T(n-2)
```

This creates a branching recursion tree:

```text
        n
      /   \
   n-1   n-2
   / \    / \
 ...
```

The number of function calls grows exponentially.

The complexity is roughly:

```text
O(k^n)
```

where:

```text
k = number of recursive calls per frame
```

For Fibonacci:

```text
k = 2
```

Therefore:

```text
O(2^n)
```

---

# Why Dynamic Programming is Better

To avoid recalculating the same Fibonacci numbers repeatedly, developers use **Dynamic Programming (Memoization)**.

Memoization stores previously computed results and reuses them whenever needed.

This reduces the complexity from:

```text
O(2^n)
```

to:

```text
O(n)
```

which is dramatically faster for large values of `n`.

---

# Summary

### Recursive Fibonacci

```text
F(n) = F(n-1) + F(n-2)
```

### Recurrence Relation

```text
T(n) = T(n-1) + T(n-2) + O(1)
```

### Actual Complexity

```text
O(1.618^n)
```

### Commonly Written As

```text
O(2^n)
```

### Reason

```text
- Two recursive calls at each step
- Exponentially growing recursion tree
- Repeated calculations of the same subproblems
```

### Space Complexity

```text
O(n)
```

### Optimized Solution

```text
Dynamic Programming (Memoization)

Time Complexity  : O(n)
Space Complexity : O(n)
```

---

# 6. Reverse Array Using Recursion

```java
class Solution {

    public void reverse(int[] arr, int n) {
        reverse(arr, 0, n - 1);
    }

    private void reverse(int[] arr, int left, int right) {

        // Entire array reversed
        if (left >= right) return;

        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        // Reverse remaining middle portion
        reverse(arr, left + 1, right - 1);
    }
}
```

### Interview Explanation

**State:**

* `left`
* `right`

**Task:**

* Reverse subarray from `left` to `right`

**Observation:**

* After swapping outer elements, only middle part remains.

**Smaller Problem:**

```text
reverse(left+1, right-1)
```

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 7. Palindrome Check

```java
class Solution {

    public boolean palindromeCheck(String s) {
        return isPalindrome(s, 0, s.length() - 1);
    }

    private boolean isPalindrome(String s, int left, int right) {

        // Entire string validated
        if (left >= right) return true;

        // Mismatch found
        if (s.charAt(left) != s.charAt(right))
            return false;

        // Verify remaining substring
        return isPalindrome(s, left + 1, right - 1);
    }
}
```

### Interview Explanation

**State:**

* `left`
* `right`

**Task:**

* Check if substring between `left` and `right` is palindrome

**Observation:**

* If outer characters match, only inner substring needs checking.

**Smaller Problem:**

```text
isPalindrome(left+1, right-1)
```

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# Quick Revision Table

| Problem          | Recurrence              | TC     | SC   |
| ---------------- | ----------------------- | ------ | ---- |
| Print 1 → N      | print(i+1)              | O(N)   | O(N) |
| Print N → 1      | print(n-1)              | O(N)   | O(N) |
| Sum of N Numbers | n + Sum(n-1)            | O(N)   | O(N) |
| Factorial        | n × Fact(n-1)           | O(N)   | O(N) |
| Fibonacci        | Fib(n-1)+Fib(n-2)       | O(2^N) | O(N) |
| Reverse Array    | Reverse(left+1,right-1) | O(N)   | O(N) |
| Palindrome Check | Check(left+1,right-1)   | O(N)   | O(N) |

---

# Important Interview Formula

For most recursion problems:

```text
(For tail resursion like find factorial of a number)
TC = Number of recursive calls × Work done per call

SC = Maximum recursion depth
```
