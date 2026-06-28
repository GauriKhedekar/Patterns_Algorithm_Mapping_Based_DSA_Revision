# String Patterns - Striver A2Z DSA Sheet

A quick revision guide to recognize the underlying pattern before solving String problems.

---

# 1. Character Traversal Pattern

## 💡 Idea

Traverse the string once while maintaining some state.

### Problems

* Largest Odd Number in a String
* Maximum Nesting Depth of Parentheses
* Remove Outermost Parentheses

### General Approach

* Scan the string from left to right.
* Maintain variables such as:

  * Counter
  * Depth
  * Answer
* Update the state based on the current character.

### Examples

**Largest Odd Number**

* Find the last odd digit.
* Return substring from `0` to that index.

**Maximum Nesting Depth**

* Increment depth on `'('`
* Decrement depth on `')'`
* Track maximum depth.

**Remove Outermost Parentheses**

* Increase depth after `'('`
* Decrease depth before `')'`
* Include characters only when depth belongs to an inner primitive.

### Time Complexity

```text
O(n)
```

---

# 2. Two Pointer Pattern

## 💡 Idea

Use two pointers to compare characters or process words.

### Problems

* Palindrome Check
* Reverse Every Word
* Reverse Words in a String

### General Approach

Maintain

```text
left
right
```

Operations may include

* Compare characters
* Reverse a word
* Skip extra spaces
* Build answer

### Common Techniques

* Skip leading/trailing spaces
* Reverse characters
* Reverse entire string
* Reverse individual words

### Time Complexity

```text
O(n)
```

---

# 3. Hashing Pattern

## 💡 Idea

Store frequencies or mappings for fast lookup.

### Problems

* Isomorphic Strings
* Anagram
* Sort Characters by Frequency

### General Approach

Use

* HashMap
* Frequency Array (`26` / `128` / `256`)

### Applications

**Frequency Counting**

```text
character → count
```

**Character Mapping**

```text
character1 → character2
```

For Isomorphic Strings

* Mapping must be one-to-one.
* Check both directions.

### Time Complexity

```text
O(n)
```

---

# 4. Prefix Matching Pattern

## 💡 Idea

Compare strings from the beginning.

### Problems

* Longest Common Prefix
* Rotate String

### General Approach

Start from index `0`.

Stop when the first mismatch occurs.

### Rotation Trick

Instead of checking every rotation

```text
(s + s).contains(goal)
```

### Time Complexity

```text
O(n)
```

---

# 5. Parsing Pattern

## 💡 Idea

Convert one representation into another.

### Problems

* Roman to Integer
* String to Integer (atoi)

### General Approach

Read characters one by one.

Maintain

```text
result
sign
currentNumber
```

Carefully handle

* Leading spaces
* '+' / '-'
* Overflow
* Invalid characters

### Roman Numerals

Compare

```text
currentValue

nextValue
```

If

```text
current < next
```

Subtract.

Else

Add.

---

# 6. Expand Around Center Pattern

## 💡 Idea

Every palindrome expands from its center.

### Problems

* Longest Palindromic Substring

### General Approach

For every index

Expand

**Odd Length**

```text
(i)
```

**Even Length**

```text
(i, i+1)
```

Continue expanding while

```text
left >= 0
right < n
s[left] == s[right]
```

Track the longest palindrome.

### Time Complexity

```text
O(n²)
```

---

# 7. Brute Force + Incremental Frequency Pattern

## 💡 Idea

Generate substrings while updating frequencies incrementally.

### Problems

* Sum of Beauty of All Substrings

### General Approach

* Fix starting index.
* Extend ending index.
* Update frequency array.
* Compute

```text
beauty = maxFrequency - minFrequency
```

Avoid recomputing frequencies from scratch.

### Time Complexity

```text
O(n² × 26)
```

---

# 8. Mathematical Counting Pattern

## 💡 Idea

Use formulas instead of generating all possibilities.

### Problems

* Count Number of Substrings

### General Approach

For a string of length `n`

```text
Number of Substrings = n × (n + 1) / 2
```

No enumeration required.

### Time Complexity

```text
O(1)
```

---

# 9. Stack / Balance Simulation Pattern

## 💡 Idea

Track nesting depth without using an explicit stack whenever possible.

### Problems

* Remove Outermost Parentheses
* Maximum Nesting Depth

### General Approach

Maintain

```text
depth
```

Rules

```text
'('

↓

depth++

')'

↓

depth--
```

Use the current depth to decide whether to include characters.

### Time Complexity

```text
O(n)
```

---

# 10. Simulation Pattern

## 💡 Idea

Implement exactly what the problem statement describes.

### Problems

* Reverse Words
* Roman to Integer
* atoi

### General Approach

Read characters sequentially.

Simulate every required operation.

Be careful with

* Spaces
* Signs
* Punctuation
* Word boundaries
* Overflow

---

# 📌 Final Revision Map

| Pattern                             | Problems                                                                |
| ----------------------------------- | ----------------------------------------------------------------------- |
| Character Traversal                 | Largest Odd Number, Maximum Nesting Depth, Remove Outermost Parentheses |
| Two Pointer                         | Palindrome Check, Reverse Words, Reverse Every Word                     |
| Hashing                             | Isomorphic Strings, Anagram, Sort Characters by Frequency               |
| Prefix Matching                     | Longest Common Prefix, Rotate String                                    |
| Parsing                             | Roman to Integer, String to Integer (atoi)                              |
| Expand Around Center                | Longest Palindromic Substring                                           |
| Brute Force + Incremental Frequency | Sum of Beauty of All Substrings                                         |
| Mathematical Counting               | Count Number of Substrings                                              |
| Stack / Balance Simulation          | Remove Outermost Parentheses, Maximum Nesting Depth                     |
| Simulation                          | Reverse Words, Roman to Integer, atoi                                   |

---

# 🎯 Pattern Recognition Guide

| If the question asks...                           | Think...                            |
| ------------------------------------------------- | ----------------------------------- |
| Scan characters while maintaining a counter/state | Character Traversal                 |
| Compare from both ends or process words           | Two Pointers                        |
| Count frequencies or map characters               | Hashing                             |
| Compare strings from the beginning                | Prefix Matching                     |
| Convert formatted strings into numbers            | Parsing                             |
| Find the longest palindrome                       | Expand Around Center                |
| Evaluate every substring efficiently              | Brute Force + Incremental Frequency |
| Count substrings without generating them          | Mathematical Counting               |
| Track nested parentheses                          | Stack / Balance Simulation          |
| Follow the exact operations in the statement      | Simulation                          |

---

# 🚀 The 10 Master String Patterns

1. **Character Traversal** → Scan once while maintaining counters/state.
2. **Two Pointers** → Compare or process characters/words efficiently.
3. **Hashing** → Frequency counting or character mapping.
4. **Prefix Matching** → Compare strings from the beginning.
5. **Parsing** → Convert formatted strings into values.
6. **Expand Around Center** → Generate palindromes efficiently.
7. **Brute Force + Incremental Frequency** → Extend substrings while updating frequencies.
8. **Mathematical Counting** → Use formulas instead of enumeration.
9. **Stack / Balance Simulation** → Track nesting depth or balance.
10. **Simulation** → Implement the process exactly as described.

---

# ⭐ Interview Recognition Checklist

Before solving a String problem, ask yourself:

* ✅ Am I simply scanning characters? → **Character Traversal**
* ✅ Do I need two indices? → **Two Pointers**
* ✅ Am I counting or mapping characters? → **Hashing**
* ✅ Am I comparing prefixes? → **Prefix Matching**
* ✅ Am I converting a string into another format? → **Parsing**
* ✅ Does the problem involve palindromes? → **Expand Around Center**
* ✅ Do I need information for every substring? → **Brute Force + Frequency**
* ✅ Can the answer be computed using a formula? → **Mathematical Counting**
* ✅ Are balanced parentheses involved? → **Stack / Balance Simulation**
* ✅ Does the problem require following a sequence of operations exactly? → **Simulation**

> **Rule of Thumb:** First identify what the problem asks you to do—scan, compare, count, parse, expand, or simulate. That immediately points you to the correct string pattern.
