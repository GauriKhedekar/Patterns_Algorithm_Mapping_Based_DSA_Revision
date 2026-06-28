# Linked List Patterns - Striver A2Z DSA Sheet

A quick revision guide to recognize the underlying pattern before solving Linked List problems.

> **Golden Rule:** Most Linked List problems are about **pointer manipulation**. Before coding, draw the nodes and pointers on paper.

---

# 1. Basic Traversal Pattern

## 💡 Idea

Traverse the Linked List node by node while maintaining the required information.

### Problems

- Introduction to Singly Linked List
- Introduction to Doubly Linked List
- Find Length of Linked List
- Search in Linked List

### General Approach

Start from

```text
temp = head
```

Traverse until

```text
temp == null
```

Update required information

- Count nodes
- Search element
- Print values
- Compute sum

### Time Complexity

```text
O(n)
```

### Space Complexity

```text
O(1)
```

---

# 2. Head Manipulation Pattern

## 💡 Idea

Only the head node is modified.

### Problems

- Insert at Head
- Delete Head
- Insert Before Head (DLL)

### General Approach

### Insertion

```text
newNode.next = head
head = newNode
```

### Deletion

```text
head = head.next
```

### Doubly Linked List

Update both

```text
next
prev
```

pointers carefully.

### Time Complexity

```text
O(1)
```

---

# 3. Pointer Reversal Pattern

## 💡 Idea

Reverse the direction of pointers.

### Problems

- Reverse Linked List (Iterative)
- Reverse Linked List (Recursive)
- Reverse Doubly Linked List

### General Approach

Maintain

```text
prev
curr
next
```

For every node

1. Save next node.
2. Reverse current pointer.
3. Move all pointers forward.

### Recursive Version

- Reverse remaining list first.
- Attach current node afterwards.

### Doubly Linked List

Swap

```text
next
prev
```

for every node.

### Time Complexity

```text
O(n)
```

### Space Complexity

Iterative

```text
O(1)
```

Recursive

```text
O(n)
```

---

# 4. Fast & Slow Pointer (Tortoise-Hare)

## 💡 Idea

Move one pointer twice as fast as the other.

### Problems

- Middle of Linked List
- Detect Loop
- Find Starting Point of Loop
- Length of Loop
- Delete Middle Node

### General Approach

Maintain

```text
slow
fast
```

Movement

```text
slow -> 1 step

fast -> 2 steps
```

### Applications

**Middle Node**

```text
Slow reaches the middle.
```

**Cycle Detection**

```text
Slow and Fast eventually meet.
```

**Cycle Start**

```text
Move one pointer to head.

Move both one step.

Meeting point = Start of cycle.
```

**Loop Length**

```text
Traverse one complete cycle after meeting.
```

**Delete Middle**

Track

```text
previous
```

node while moving.

### Time Complexity

```text
O(n)
```

---

# 5. Two Pointer Gap Pattern

## 💡 Idea

Maintain a fixed distance between two pointers.

### Problems

- Remove Nth Node from End

### General Approach

Move

```text
fast
```

ahead by

```text
N
```

steps.

Now move

```text
slow
fast
```

together.

When

```text
fast
```

reaches the end,

```text
slow
```

is just before the required node.

Use a

```text
Dummy Node
```

to simplify edge cases.

### Time Complexity

```text
O(n)
```

---

# 6. Half Processing Pattern

## 💡 Idea

Process only half of the Linked List.

### Problems

- Check if Linked List is Palindrome

### General Approach

Steps

1. Find middle.
2. Reverse second half.
3. Compare both halves.
4. (Optional) Restore original list.

Pattern Combination

```text
Fast & Slow Pointer

+

Pointer Reversal
```

### Time Complexity

```text
O(n)
```

### Space Complexity

```text
O(1)
```

---

# 7. List Rearrangement Pattern

## 💡 Idea

Rearrange nodes without changing their values.

### Problems

- Segregate Odd and Even Nodes

### General Approach

Maintain two chains

```text
Odd List

Even List
```

Finally connect

```text
Odd Tail -> Even Head
```

No extra nodes are created.

### Time Complexity

```text
O(n)
```

### Space Complexity

```text
O(1)
```

---

# 8. Pointer Manipulation / Simulation Pattern

## 💡 Idea

Carefully update pointers while preserving access to remaining nodes.

### Problems

- Insert/Delete operations
- Delete Middle Node
- Reverse DLL
- Segregate Odd-Even Nodes

### General Approach

Always follow this order

```text
1. Save important pointers

2. Modify links

3. Move pointers
```

⚠️ Never overwrite a pointer before saving the next node.

### Time Complexity

Depends on the operation.

---

# 📌 Final Revision Map

| Pattern | Problems |
|----------|----------|
| Basic Traversal | Length, Search, Introduction to SLL, Introduction to DLL |
| Head Manipulation | Insert Head, Delete Head, Insert Before Head (DLL) |
| Pointer Reversal | Reverse LL (Iterative), Reverse LL (Recursive), Reverse DLL |
| Fast & Slow Pointer | Middle, Detect Loop, Loop Start, Loop Length, Delete Middle |
| Two Pointer Gap | Remove Nth Node from End |
| Half Processing | Palindrome Linked List |
| List Rearrangement | Odd-Even Linked List |
| Pointer Manipulation | Insert/Delete, Reverse DLL, Delete Middle, Odd-Even Rearrangement |

---

# 🎯 Pattern Recognition Guide

| If the question asks... | Think... |
|--------------------------|----------|
| Traverse every node | Basic Traversal |
| Modify only the first node | Head Manipulation |
| Reverse the list | Pointer Reversal |
| Find middle or detect cycle | Fast & Slow Pointer |
| Find kth node from end | Two Pointer Gap |
| Compare first half with second half | Half Processing |
| Separate nodes into groups | List Rearrangement |
| Update links carefully | Pointer Manipulation |

---

# 🚀 The 8 Master Linked List Patterns

## 1. Basic Traversal

Traverse node by node while maintaining required information.

**Problems**

- Length
- Search
- Traversal

---

## 2. Head Manipulation

Modify only the head pointer.

**Problems**

- Insert Head
- Delete Head
- Insert Before Head (DLL)

---

## 3. Pointer Reversal

Reverse links using

```text
prev
curr
next
```

**Problems**

- Reverse LL
- Reverse DLL

---

## 4. Fast & Slow Pointer (Tortoise-Hare)

Move one pointer twice as fast.

**Problems**

- Middle
- Detect Loop
- Loop Start
- Loop Length
- Delete Middle

---

## 5. Two Pointer Gap

Maintain a fixed gap between two pointers.

**Problems**

- Remove Nth Node from End

---

## 6. Half Processing

Process only half of the Linked List.

**Problems**

- Palindrome Linked List

---

## 7. List Rearrangement

Split into logical groups and reconnect.

**Problems**

- Odd-Even Linked List

---

## 8. Pointer Manipulation / Simulation

Safely modify `next` and `prev` pointers.

**Problems**

- Insert/Delete
- Reverse DLL
- Delete Middle
- Odd-Even Rearrangement

---

# ⭐ Common Pattern Combinations

Many interview problems are combinations of multiple patterns.

| Problem | Combination |
|----------|-------------|
| Palindrome Linked List | Fast & Slow Pointer + Pointer Reversal |
| Find Loop Start | Cycle Detection + Two Pointer Movement |
| Delete Middle Node | Fast & Slow Pointer + Pointer Manipulation |
| Reverse Doubly Linked List | Pointer Reversal + Pointer Manipulation |
| Odd-Even Linked List | Traversal + List Rearrangement |
| Remove Nth Node from End | Two Pointer Gap + Pointer Manipulation |

---

# 💡 Interview Tips

### Always draw the Linked List.

Even a rough diagram helps avoid pointer mistakes.

### Save pointers before changing them.

```text
next = curr.next
```

should almost always come before modifying `curr.next`.

### Use a Dummy Node whenever deletion may affect the head.

It removes most edge cases.

### Master these four techniques first

- Fast & Slow Pointer
- Pointer Reversal
- Two Pointer Gap
- Pointer Manipulation

These appear in the majority of Linked List interview questions.

---

# 📝 Final Takeaway

Most Linked List interview questions are **not entirely new algorithms**. They are combinations of a few fundamental pointer techniques.

If you can quickly recognize whether the problem requires:

- Traversal
- Reversal
- Fast & Slow Pointer
- Gap Technique
- Pointer Manipulation

then implementing the solution becomes much easier.
