# Binary Search Patterns - Striver A2Z DSA Sheet

> A quick revision guide for recognizing Binary Search patterns.
> **Golden Rule:** Before writing code, identify **what you're binary searching on**:
>
> * Value?
> * Boundary?
> * Property?
> * Answer?
> * Partition?
> * Matrix?

---

# 1. Classic Binary Search (Exact Search)

## 💡 Idea

Search for an exact value in a sorted array.

### Problems

* Search X in Sorted Array

### General Approach

* Maintain `low` and `high`.
* Compute `mid`.
* Compare `arr[mid]` with target.
* Search left/right accordingly.

### Template

```java
while(low <= high){
    int mid = low + (high-low)/2;

    if(arr[mid] == target)
        return mid;
    else if(arr[mid] < target)
        low = mid + 1;
    else
        high = mid - 1;
}
return -1;
```

**Time:** `O(log n)`

---

# 2. Boundary Search (Lower Bound / Upper Bound)

## 💡 Idea

Instead of finding an element, find the **first/last valid position**.

### Problems

* Lower Bound
* Upper Bound
* Search Insert Position
* Floor & Ceil
* First and Last Occurrence
* Count Occurrences

### General Approach

Maintain an answer variable.

Whenever current index satisfies the condition

* store answer
* continue searching toward boundary

### Conditions

| Problem          | Condition                |
| ---------------- | ------------------------ |
| Lower Bound      | first `>= x`             |
| Upper Bound      | first `> x`              |
| Floor            | largest `<= x`           |
| Ceil             | smallest `>= x`          |
| First Occurrence | move left after finding  |
| Last Occurrence  | move right after finding |

---

# 3. Binary Search on Rotated Array

## 💡 Idea

At least one half is always sorted.

### Problems

* Search in Rotated Sorted Array-I
* Search in Rotated Sorted Array-II
* Find Minimum
* Rotation Count

### General Approach

Every iteration

1. Determine which half is sorted.
2. Check if target belongs there.
3. Otherwise search the other half.

Duplicates

Skip equal elements when necessary.

---

# 4. Binary Search on Property

## 💡 Idea

Search for a property instead of an element.

### Problems

* Single Element
* Peak Element

### General Approach

Examples

### Single Element

Before answer

```
Pairs start at even index
```

After answer

```
Pairs start at odd index
```

---

### Peak Element

Compare

```
mid
mid+1
```

Move toward increasing slope.

---

# 5. Binary Search on Answer (Most Important)

## 💡 Idea

Don't search the array.

Search the **answer**.

### Problems

* Square Root
* Nth Root
* Koko Eating Bananas
* Minimum Days to Make Bouquets
* Smallest Divisor
* Ship Packages
* Kth Missing Positive
* Aggressive Cows
* Book Allocation
* Split Array Largest Sum
* Painter's Partition
* Minimize Maximum Distance to Gas Station

---

## Recognition Checklist

If the problem asks

* Minimum possible...
* Maximum possible...
* Smallest...
* Largest...
* Minimize...
* Maximize...
* Is it possible?
* Can we finish within X?

➡️ Think **Binary Search on Answer**.

---

## General Template

```java
int low = minimumPossibleAnswer;
int high = maximumPossibleAnswer;
int ans = -1;

while(low <= high){

    int mid = low + (high-low)/2;

    if(isPossible(mid)){
        ans = mid;
        high = mid - 1;     // minimum answer
    }
    else{
        low = mid + 1;
    }
}

return ans;
```

---

## Common Answer Range

### Low

* 1
* minimum element
* maximum element
* largest book

### High

* sum of array
* maximum pile
* total distance

---

## Common Helper Functions

### Counting

* Students required
* Days required
* Bouquets formed
* Cows placed

### Simulation

* Can ship?
* Can place cows?
* Can divide?

---

# ⭐ Hard Pattern 1 : Aggressive Cows

## Answer Space

```
Minimum distance = 1

Maximum distance =
last stall - first stall
```

### Helper

```java
boolean canPlace(int[] stalls,int cows,int dist){

    int placed = 1;
    int last = stalls[0];

    for(int i=1;i<stalls.length;i++){

        if(stalls[i]-last >= dist){
            placed++;
            last = stalls[i];
        }

        if(placed>=cows)
            return true;
    }

    return false;
}
```

### Binary Search

```java
Arrays.sort(stalls);

int low = 1;
int high = stalls[n-1]-stalls[0];

while(low<=high){

    int mid=(low+high)/2;

    if(canPlace(stalls,cows,mid))
        low=mid+1;
    else
        high=mid-1;
}

return high;
```

**Trick**

> We want the **largest minimum distance**.

---

# ⭐ Hard Pattern 2 : Book Allocation

## Answer Space

```
Low = largest book

High = sum of all pages
```

### Helper

```java
boolean canAllocate(int[] arr,int students,int pages){

    int count=1;
    int sum=0;

    for(int x:arr){

        if(sum+x<=pages){
            sum+=x;
        }
        else{
            count++;
            sum=x;
        }

        if(count>students)
            return false;
    }

    return true;
}
```

**Remember**

```
Maximum book

↓

Minimum possible answer
```

---

# ⭐ Hard Pattern 3 : Minimize Maximum Distance to Gas Station

## Trick

Binary Search on **Double Answer**

Answer isn't integer.

Instead

```
while(high-low > 1e-6)
```

### Helper

```java
int requiredStations(int[] arr,double dist){

    int count=0;

    for(int i=1;i<arr.length;i++){

        count += (int)((arr[i]-arr[i-1])/dist);

        if((arr[i]-arr[i-1])%dist==0)
            count--;
    }

    return count;
}
```

Binary Search

```
if(required<=k)

search left

else

search right
```

**Remember**

Floating point Binary Search uses

```
while(high-low > 1e-6)
```

instead of

```
low<=high
```

---

# ⭐ Hard Pattern 4 : Median of Two Sorted Arrays

## Idea

Never merge arrays.

Partition both arrays.

```
Left Half

<=

Right Half
```

Maintain

```
cut1

cut2
```

such that

```
cut1+cut2=(n1+n2+1)/2
```

Conditions

```
left1<=right2

&&

left2<=right1
```

If true

Median found.

Else

Adjust partition.

**Time**

```
O(log(min(n,m)))
```

---

# 6. Binary Search on 2D Matrix

## Problems

* Row with Maximum 1s
* Search Matrix
* Search Matrix II
* Peak II
* Matrix Median

---

## Pattern A : Row Wise Binary Search

### Problem

Row with Maximum 1s

Approach

Binary search each row.

Find first one.

Maximum count wins.

---

## Pattern B : Flatten Matrix

### Problem

Search Matrix

Convert

```
row = mid / m

col = mid % m
```

Apply normal Binary Search.

---

## Pattern C : Staircase Search

### Problem

Search Matrix II

Start from

```
Top Right
```

Move

```
Current > Target

↓

Left

Current < Target

↓

Down
```

Time

```
O(n+m)
```

---

## Pattern D : Binary Search on Columns

### Problem

Peak II

Choose middle column.

Find maximum element.

Compare neighbours.

Move toward larger neighbour.

---

## Pattern E : Binary Search on Answer

### Problem

Matrix Median

Binary search over values.

For every value

Count

```
Elements <= mid
```

using Lower Bound in every row.

---

# Binary Search on Two Sorted Arrays

## Problems

* Median of Two Sorted Arrays
* Kth Element of Two Sorted Arrays

## Trick

Always Binary Search on the **smaller array**.

Maintain partitions.

Never merge arrays.

Complexity

```
O(log(min(n,m)))
```

---

# 📌 Final Revision Map

| Pattern                 | Problems                                                                                                                                       |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Classic Binary Search   | Search X                                                                                                                                       |
| Boundary Search         | Lower Bound, Upper Bound, Search Insert, Floor & Ceil, First/Last Occurrence, Count Occurrences                                                |
| Rotated Array           | Search Rotated I, Search Rotated II, Minimum, Rotation Count                                                                                   |
| Property Search         | Single Element, Peak Element                                                                                                                   |
| Binary Search on Answer | Square Root, Nth Root, Koko, Bouquets, Divisor, Ship Packages, Aggressive Cows, Book Allocation, Split Array, Painter's Partition, Gas Station |
| Two Sorted Arrays       | Median, Kth Element                                                                                                                            |
| 2D Binary Search        | Row Max 1s, Search Matrix, Matrix II, Peak II, Matrix Median                                                                                   |

---

# 🚀 Master Binary Search Templates

1. Classic Binary Search
2. Lower Bound / Upper Bound
3. Rotated Array
4. Property Search
5. Binary Search on Answer (`isPossible()`)
6. Partition Binary Search (Median/Kth Element)
7. Matrix Binary Search

---

# ⭐ Most Important Interview Tricks

* **Minimum possible answer** → `high = mid - 1`
* **Maximum possible answer** → `low = mid + 1`
* Always derive **Low** and **High** before coding.
* Write `isPossible(mid)` first for answer-space problems.
* For floating-point answers (Gas Station), use:

```java
while(high - low > 1e-6)
```

instead of `low <= high`.

* For **Median/Kth Element**, **never merge arrays**. Use partition-based Binary Search on the smaller array.

* For **Nth Root**, avoid overflow by multiplying step-by-step and stopping early if the product exceeds the target.

# Binary Search on 2D Arrays - Striver A2Z Revision Notes

Unlike 1D Binary Search, the algorithm for 2D matrices depends entirely on the **sorting property of the matrix**.

> **Golden Rule:** Before solving any 2D Binary Search problem, first identify **how the matrix is sorted**.

---

# Pattern 1: Binary Search in Every Row

## 💡 Matrix Property

* Every row is individually sorted.
* Rows are independent.
* Need information from each row.

### Problems

* Find Row with Maximum 1's

### General Approach

* Binary search every row independently.
* Find the **first occurrence of 1**.
* Count the number of 1's.

```text
Count = Columns - FirstOneIndex
```

Return the row having the maximum count.

### Time Complexity

```text
O(n log m)
```

### Space Complexity

```text
O(1)
```

---

# Pattern 2: Treat Matrix as a 1D Sorted Array

## 💡 Matrix Property

The entire matrix is globally sorted.

```text
Last element of row i < First element of row i+1
```

Example

```text
1   3   5
7   9   11
13  15  17
```

Flattened view

```text
1 3 5 7 9 11 13 15 17
```

### Problems

* Search in a 2D Matrix

### General Approach

Imagine the matrix as one sorted array.

Convert the 1D index into row and column.

```java
row = mid / columns;
col = mid % columns;
```

Then perform a normal Binary Search.

### Time Complexity

```text
O(log(n × m))
```

### Space Complexity

```text
O(1)
```

---

# Pattern 3: Staircase Search

## 💡 Matrix Property

* Every row is sorted.
* Every column is sorted.
* Entire matrix is **NOT** globally sorted.

Example

```text
1   4   7
2   5   8
3   6   9
```

Flattening **does not work** here.

### Problems

* Search in 2D Matrix II

### General Approach

Start from

```text
Top Right
```

or

```text
Bottom Left
```

Reason

```text
Left  → Smaller
Down  → Larger
```

Decision

```text
Current > Target

↓

Move Left

Current < Target

↓

Move Down
```

### Time Complexity

```text
O(n + m)
```

### Space Complexity

```text
O(1)
```

---

# Pattern 4: Binary Search on Columns

## 💡 Matrix Property

Need to find a **Peak Element**.

### Problems

* Find Peak Element II

### General Approach

1. Choose the middle column.
2. Find the maximum element in that column.
3. Compare it with its left and right neighbours.
4. Move toward the larger neighbour.
5. Repeat until a peak is found.

This is exactly the 2D version of the 1D Peak Element problem.

### Time Complexity

```text
O(n log m)
```

### Space Complexity

```text
O(1)
```

---

# Pattern 5: Binary Search on Answer (Value Space)

## 💡 Matrix Property

Rows are sorted.

Need to find

* Median
* Kth Smallest
* Similar value-based answers

### Problems

* Matrix Median

### General Approach

Instead of searching indices, search the **value range**.

Choose

```text
Low = Minimum element

High = Maximum element
```

For every candidate value

```text
mid
```

Count

```text
Elements <= mid
```

using **Upper Bound** (or Lower Bound depending on implementation) in every row.

If enough elements are less than or equal to `mid`

→ Search Left

Else

→ Search Right

### Time Complexity

```text
O(log(Value Range) × n × log m)
```

### Space Complexity

```text
O(1)
```

---

# 📌 Recognition Flowchart

```text
                         MATRIX
                            │
                            ▼
          Is the entire matrix globally sorted?
                            │
               Yes ─────────► Flatten Matrix
                            │
               No
                            ▼
      Are rows and columns individually sorted?
                            │
                Yes
                            ▼
        Searching for an element?
           │                     │
           ▼                     ▼
 Staircase Search       Peak Element II
                         (Column Binary Search)

                            │
                            ▼
      Need Median / Kth Smallest Value?
                            │
                           Yes
                            ▼
            Binary Search on Answer

                            │
                            ▼
     Need information from each row?
                            │
                           Yes
                            ▼
          Binary Search Every Row
```

---

# 📊 Final Revision Map

| Pattern                 | Matrix Property                | Problems                  | Time Complexity             |
| ----------------------- | ------------------------------ | ------------------------- | --------------------------- |
| Binary Search Every Row | Every row sorted independently | Find Row with Maximum 1's | **O(n log m)**              |
| Flatten Matrix          | Entire matrix globally sorted  | Search in 2D Matrix       | **O(log(n×m))**             |
| Staircase Search        | Rows & Columns sorted          | Search in Matrix II       | **O(n+m)**                  |
| Column Binary Search    | Peak search                    | Find Peak Element II      | **O(n log m)**              |
| Binary Search on Answer | Search over value space        | Matrix Median             | **O(log(range) × n log m)** |

---

# 🚀 Interview Recognition Checklist

Before solving any 2D Binary Search problem, ask these questions:

### ✅ Can I flatten the matrix into one sorted array?

→ Use **Flatten Matrix Binary Search**

### ✅ Are both rows and columns sorted?

* Searching an element → **Staircase Search**
* Finding a peak → **Column Binary Search**

### ✅ Am I searching for a value (Median/Kth Smallest)?

→ Use **Binary Search on Answer**

### ✅ Do I need to process every row independently?

→ Use **Binary Search in Every Row**

---

# ⭐ 5 Master Patterns to Memorize

1. **Binary Search Every Row** → Find Row with Maximum 1's
2. **Flatten Matrix** → Search in 2D Matrix
3. **Staircase Search** → Search in Matrix II
4. **Column Binary Search** → Find Peak Element II
5. **Binary Search on Answer** → Matrix Median

> **Rule of Thumb:** Always identify the matrix's sorting property first. Once the property is known, the correct Binary Search pattern becomes obvious.
