# 32. Binary Search Variant: Bounds Pattern

## Problems

- Lower Bound
- Upper Bound
- Search Insert Position
- Floor and Ceil in Sorted Array
- First and Last Occurrence

## Core Idea

Instead of searching for an exact element, search for the boundary where a condition becomes true.

## Interview Explanation

### State

```text
low
high
mid
answer
```

### Task

Find a position satisfying a condition.

### Observation

Classic Binary Search:

```text
Find target
```

Bounds Binary Search:

```text
Find first position
or
Find last position
```

Think:

```text
Boundary Search
```

rather than

```text
Exact Search
```

## Recognition Clues

```text
First occurrence
Last occurrence
Lower bound
Upper bound
Insert position
Floor
Ceil
Sorted array
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

---

# Lower Bound Pattern

## Problems

- Lower Bound
- Search Insert Position

## Core Idea

Find the first index where:

```text
arr[i] >= target
```

## Interview Explanation

### State

```text
answer = n
```

### Observation

If:

```text
arr[mid] >= target
```

mid can be answer.

But there may be a smaller valid index.

Move left.

## Recognition Clues

```text
First >= target
Insert position
Lower bound
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

## Java Code

```java
public static int lowerBound(int[] arr, int target){

    int n = arr.length;

    int low = 0;
    int high = n - 1;

    int ans = n;

    while(low <= high){

        int mid = low + (high - low) / 2;

        if(arr[mid] >= target){

            ans = mid;
            high = mid - 1;
        }
        else{
            low = mid + 1;
        }
    }

    return ans;
}
```

## Quick Revision

```text
First >= target

Valid answer found

Move left
```

---

# Upper Bound Pattern

## Problems

- Upper Bound

## Core Idea

Find first index where:

```text
arr[i] > target
```

## Interview Explanation

### State

```text
answer = n
```

### Observation

If:

```text
arr[mid] > target
```

mid may be answer.

Move left to find smaller valid index.

## Recognition Clues

```text
First > target
Upper bound
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

## Java Code

```java
public static int upperBound(int[] arr, int target){

    int n = arr.length;

    int low = 0;
    int high = n - 1;

    int ans = n;

    while(low <= high){

        int mid = low + (high - low) / 2;

        if(arr[mid] > target){

            ans = mid;
            high = mid - 1;
        }
        else{
            low = mid + 1;
        }
    }

    return ans;
}
```

## Quick Revision

```text
First > target

Valid answer

Move left
```

---

# Search Insert Position Pattern

## Problems

- Search Insert Position

## Core Idea

Search Insert Position is exactly Lower Bound.

## Interview Explanation

### Observation

Position where element should be inserted:

```text
First position
>= target
```

which is:

```text
Lower Bound
```

## Recognition Clues

```text
Insert position
Sorted array
Maintain order
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

## Java Code

```java
class Solution {

    public int searchInsert(
            int[] nums,
            int target) {

        int low = 0;
        int high = nums.length - 1;

        int ans = nums.length;

        while(low <= high){

            int mid =
                low + (high - low) / 2;

            if(nums[mid] >= target){

                ans = mid;
                high = mid - 1;
            }
            else{
                low = mid + 1;
            }
        }

        return ans;
    }
}
```

## Quick Revision

```text
Search Insert Position

=

Lower Bound
```

---

# Floor and Ceil Pattern

## Problems

- Floor and Ceil in Sorted Array

## Core Idea

Floor:

```text
Largest value <= target
```

Ceil:

```text
Smallest value >= target
```

## Interview Explanation

### State

```text
floor = -1
ceil = -1
```

### Observation

For Floor:

```text
arr[mid] <= target

possible answer

move right
```

For Ceil:

```text
arr[mid] >= target

possible answer

move left
```

## Recognition Clues

```text
Nearest smaller
Nearest greater
Floor
Ceil
Sorted array
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

## Java Code

### Floor

```java
public static int floor(int[] arr, int target){

    int low = 0;
    int high = arr.length - 1;

    int ans = -1;

    while(low <= high){

        int mid =
            low + (high - low) / 2;

        if(arr[mid] <= target){

            ans = arr[mid];
            low = mid + 1;
        }
        else{
            high = mid - 1;
        }
    }

    return ans;
}
```

### Ceil

```java
public static int ceil(int[] arr, int target){

    int low = 0;
    int high = arr.length - 1;

    int ans = -1;

    while(low <= high){

        int mid =
            low + (high - low) / 2;

        if(arr[mid] >= target){

            ans = arr[mid];
            high = mid - 1;
        }
        else{
            low = mid + 1;
        }
    }

    return ans;
}
```

## Quick Revision

```text
Floor

<= target
Move Right

Ceil

>= target
Move Left
```

---

# First and Last Occurrence Pattern

## Problems

- First Occurrence
- Last Occurrence
- Search Range

## Core Idea

Find left boundary and right boundary separately.

## Interview Explanation

### State

```text
answer
```

### Observation

First Occurrence:

```text
nums[mid] == target

Store answer

Move Left
```

Last Occurrence:

```text
nums[mid] == target

Store answer

Move Right
```

## Recognition Clues

```text
Duplicates
First occurrence
Last occurrence
Search range
Occurrences
```

## TC / SC

| Time | Space |
|--------|--------|
| O(log N) | O(1) |

## Java Code

### First Occurrence

```java
public static int firstOccurrence(
        int[] nums,
        int target){

    int low = 0;
    int high = nums.length - 1;

    int ans = -1;

    while(low <= high){

        int mid =
            low + (high - low) / 2;

        if(nums[mid] == target){

            ans = mid;
            high = mid - 1;
        }
        else if(nums[mid] < target){
            low = mid + 1;
        }
        else{
            high = mid - 1;
        }
    }

    return ans;
}
```

### Last Occurrence

```java
public static int lastOccurrence(
        int[] nums,
        int target){

    int low = 0;
    int high = nums.length - 1;

    int ans = -1;

    while(low <= high){

        int mid =
            low + (high - low) / 2;

        if(nums[mid] == target){

            ans = mid;
            low = mid + 1;
        }
        else if(nums[mid] < target){
            low = mid + 1;
        }
        else{
            high = mid - 1;
        }
    }

    return ans;
}
```

### Search Range

```java
class Solution {

    public int[] searchRange(
            int[] nums,
            int target) {

        int first =
            firstOccurrence(nums, target);

        int last =
            lastOccurrence(nums, target);

        return new int[]{first, last};
    }
}
```

## Quick Revision

```text
First Occurrence

Found target
Move Left

Last Occurrence

Found target
Move Right

Search Range

[first,last]
```

---

# Interview Master Shortcut

## Lower Bound

```text
First >= target
```

## Upper Bound

```text
First > target
```

## Search Insert Position

```text
Lower Bound
```

## Floor

```text
Largest <= target
```

## Ceil

```text
Smallest >= target
```

## First Occurrence

```text
Found target

Move Left
```

## Last Occurrence

```text
Found target

Move Right
```

## One-Line Recognition

```text
Sorted Array +
First/Last/Nearest/Insert

=> Binary Search on Boundaries
```

---

# Pattern 34: Rotated Sorted Array + Bounds Binary Search

---

# Problem 1: Count Occurrences in a Sorted Array

## Pattern

Bounds Binary Search

## Core Idea

Find:

* First Occurrence of target
* Last Occurrence of target

Count:

```text
Last - First + 1
```

---

## Interview Explanation

### State

```text
Array is sorted.
Duplicates may exist.
```

### Task

```text
Count total occurrences of target.
```

### Observation

```text
If we know:

First Occurrence = f
Last Occurrence = l

Then

Count = l - f + 1
```

---

## Recognition Clues

Use when:

```text
Sorted Array
Count Frequency
Find First Occurrence
Find Last Occurrence
Duplicates Present
```

---

## TC / SC

```text
TC = O(logN)
SC = O(1)
```

---

## Java Code

```java
class Solution {
    public int countOccurrences(int[] arr, int target) {
        int n = arr.length;
        int s = 0;
        int e = n - 1;
        int first = -1;

        while(s <= e){
             int m = s + (e - s) / 2;

             if(arr[m] == target){
                first = m;
                e = m - 1;
             }
             else if(arr[m] > target){
                e = m - 1;
             }
             else{
                s = m + 1;
             }
        }

        int s1 = 0;
        int e1 = n - 1;
        int last = -1;

        while(s1 <= e1){
            int m1 = s1 + (e1 - s1) / 2;

            if(arr[m1] == target){
                last = m1;
                s1 = m1 + 1;
            }
            else if(arr[m1] > target){
                 e1 = m1 - 1;
            }
            else{
                s1 = m1 + 1;
            }
        }

        if(first == -1){
            return -1;
        }

        return last - first + 1;
    }
}
```

---

## Quick Revision

```text
FIRST OCCURRENCE
Found -> Move Left

LAST OCCURRENCE
Found -> Move Right

Answer
= Last - First + 1
```

---

# Problem 2: Search in Rotated Sorted Array I

## Pattern

Pivot + Binary Search

---

## Core Idea

```text
Find Pivot

Array becomes

[Sorted Part 1]
[Sorted Part 2]

Binary Search on proper half
```

---

## Interview Explanation

### State

```text
Sorted array rotated once.
No duplicates.
```

### Task

```text
Find target index.
```

### Observation

```text
After pivot detection:

0 → Pivot
Pivot+1 → N-1

Both halves are sorted.
```

---

## Recognition Clues

```text
Rotated Sorted Array
Unique Elements
Search Target
O(logN)
```

---

## TC / SC

```text
TC = O(logN)
SC = O(1)
```

---

## Java Code

```java
class Solution {
    public int search(int[] nums, int target) {

       int n = nums.length;
       int s = 0;
       int e = n - 1;
       int pivot = -1;

       while(s <= e){

        int m = s + (e - s) / 2;

        if(m < n - 1 && nums[m] > nums[m + 1]){
            pivot = m;
            break;
        }
        else if(nums[m] >= nums[s]){
            s = m + 1;
        }
        else{
            e = m - 1;
        }
       }

       if(pivot == -1){
        return bs(nums, 0, n - 1, target);
       }

       int ans = bs(nums, 0, pivot, target);

       if(ans == -1){
        return bs(nums, pivot + 1, n - 1, target);
       }

       return ans;
    }

    public int bs(int[] nums, int s, int e, int target){

        while(s <= e){

            int m = s + (e - s) / 2;

            if(nums[m] == target){
                return m;
            }
            else if(nums[m] > target){
                e = m - 1;
            }
            else{
                s = m + 1;
            }
        }

        return -1;
    }
}
```

---

## Quick Revision

```text
STEP 1
Find Pivot

STEP 2
Binary Search Left Half

STEP 3
Binary Search Right Half
```

---

# Problem 3: Search in Rotated Sorted Array II

## Pattern

Pivot Binary Search + Duplicate Handling

---

## Core Idea

```text
Duplicates destroy sorted-half detection.

When:

arr[s] == arr[mid] == arr[e]

Shrink both sides.
```

---

## Interview Explanation

### State

```text
Rotated Sorted Array
Duplicates Present
```

### Task

```text
Return true if target exists.
```

### Observation

```text
Duplicates create ambiguity.

Remove ambiguity
by shrinking boundaries.
```

---

## Recognition Clues

```text
Rotated Array
Duplicates
Search Element
```

---

## TC / SC

```text
Worst TC = O(N)

Average TC = O(logN)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public boolean search(int[] nums, int target) {

        int n = nums.length;
        int s = 0;
        int e = n - 1;
        int pivot = -1;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(nums[s] == nums[m] && nums[m] == nums[e]){

                if(s < n - 1 && nums[s] > nums[s + 1]){
                    pivot = s;
                    break;
                }

                s++;

                if(e > 0 && nums[e] < nums[e - 1]){
                    pivot = e - 1;
                    break;
                }

                e--;
            }

            else if(m < n - 1 && nums[m] > nums[m + 1]){
                pivot = m;
                break;
            }

            else if(nums[m] >= nums[s]){
                  s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        if(pivot == -1)
            return bs(nums, 0, n - 1, target);

        boolean ans = bs(nums, 0, pivot, target);

        if(!ans){
            return bs(nums, pivot + 1, n - 1, target);
        }

        return ans;
    }

    public boolean bs(int[] nums, int s, int e, int target){

        while(s <= e){

            int m = s + (e - s) / 2;

            if(nums[m] == target){
                return true;
            }
            else if(nums[m] < target){
                s = m + 1;
            }
            else{
                e = m - 1;
            }
        }

        return false;
    }
}
```

---

## Quick Revision

```text
Duplicates?

YES

arr[s] == arr[mid] == arr[e]

=> s++
=> e--
```

---

# Problem 4: Find Minimum in Rotated Sorted Array

## Pattern

Pivot Detection

---

## Core Idea

```text
Pivot = largest element

Minimum = Pivot + 1
```

---

## Interview Explanation

### State

```text
Sorted Array Rotated
```

### Task

```text
Find minimum element.
```

### Observation

```text
Pivot divides array.

Minimum lies right after pivot.
```

---

## Recognition Clues

```text
Rotated Array
Minimum Element
```

---

## TC / SC

```text
TC = O(logN)

Duplicates Case
Worst O(N)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int findMin(int[] nums) {

        int n = nums.length;
        int s = 0;
        int e = n - 1;
        int pivot = -1;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(nums[s] == nums[m] && nums[m] == nums[e]){

                if(s < n - 1 && nums[s] > nums[s + 1]){
                    pivot = s;
                    break;
                }

                s++;

                if(e > 0 && nums[e] < nums[e - 1]){
                    pivot = e - 1;
                    break;
                }

                e--;
            }

            else if(m < n - 1 && nums[m] > nums[m + 1]){
                pivot = m;
                break;
            }

            else if(nums[m] >= nums[s]){
                s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        if(pivot == -1){
            return nums[0];
        }

        return nums[pivot + 1];
    }
}
```

---

## Quick Revision

```text
Pivot Found?

YES
Answer = pivot + 1

NO
Answer = nums[0]
```

---

# Problem 5: Find Out How Many Times Array Is Rotated

## Pattern

Pivot Detection

---

## Core Idea

```text
Rotation Count

= Index of Minimum

= Pivot + 1
```

---

## Interview Explanation

### State

```text
Sorted Array Rotated
```

### Task

```text
Find number of rotations.
```

### Observation

```text
Minimum element
appears at rotation count index.
```

---

## Recognition Clues

```text
Rotation Count
Rotated Array
Find Minimum Index
```

---

## TC / SC

```text
TC = O(logN)

Worst = O(N)
(duplicates)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int findKRotation(ArrayList<Integer> nums) {

       int n = nums.size();
       int s = 0;
       int e = n - 1;
       int pivot = -1;

       while(s <= e){

        int m = s + (e - s) / 2;

        if(nums.get(s) == nums.get(m) &&
           nums.get(m) == nums.get(e)){

            if(s < n - 1 &&
               nums.get(s) > nums.get(s + 1)){
                pivot = s;
                break;
            }

            s++;

            if(e > 0 &&
               nums.get(e) < nums.get(e - 1)){
                pivot = e - 1;
                break;
            }

            e--;
        }

        else if(m < n - 1 &&
                nums.get(m) > nums.get(m + 1)){
            pivot = m;
            break;
        }

        else if(nums.get(m) >= nums.get(s)){
            s = m + 1;
        }

        else{
            e = m - 1;
        }
       }

       return pivot + 1;
    }
}
```

---

## Quick Revision

```text
Rotation Count
=
Minimum Index
=
Pivot + 1

Example

4 5 6 7 1 2 3

Pivot = 3

Rotations = 4
```

---

# Pattern Summary

```text
COUNT OCCURRENCES
→ First + Last Occurrence

SEARCH ROTATED ARRAY
→ Pivot + Binary Search

ROTATED ARRAY II
→ Handle Duplicates

FIND MINIMUM
→ Pivot + 1

ROTATION COUNT
→ Pivot + 1
```

# Pattern 35: Binary Search on Index Properties + Binary Search on Answers (Part 2)

---

# Problem 6: Single Element in a Sorted Array

## Pattern

Binary Search on Index Properties

---

## Core Idea

Every element appears twice except one.

Observe pair formation:

```text
Before Single Element

Index: 0 1 2 3 4 5
Value: 1 1 2 2 3 3

Pairs start at EVEN index
```

```text
After Single Element

Index: 0 1 2 3 4 5 6

Value: 1 1 2 3 3 4 4

Pairs start at ODD index
```

---

## Interview Explanation

### State

```text
Sorted Array
Every element appears twice
One element appears once
```

### Task

```text
Find unique element
```

### Observation

```text
Before answer

Even index matches next index

After answer

Odd index matches previous index
```

---

## Recognition Clues

```text
Sorted Array
Pairs
Only One Unique Element
O(logN) Required
```

---

## TC / SC

```text
TC = O(logN)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int singleNonDuplicate(int[] nums) {

        int n = nums.length;

        if(n == 1) return nums[0];

        if(nums[0] != nums[1]) return nums[0];

        if(nums[n - 1] != nums[n - 2]) return nums[n - 1];

        int s = 0;
        int e = n - 1;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(m > 0 &&
               m < n - 1 &&
               nums[m] != nums[m - 1] &&
               nums[m] != nums[m + 1]){
                return nums[m];
            }

            else if(
                (m % 2 == 0 &&
                 m < n - 1 &&
                 nums[m] == nums[m + 1])

                 ||

                (m % 2 == 1 &&
                 m > 0 &&
                 nums[m] == nums[m - 1])
            ){
                 s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        return -1;
    }
}
```

---

## Quick Revision

```text
EVEN INDEX

Should match NEXT

ODD INDEX

Should match PREVIOUS

Condition breaks?

Unique element side found
```

---

# Problem 7: Find Peak Element

## Pattern

Binary Search on Slope

---

## Core Idea

```text
If mid < mid+1

You are on increasing slope

Move Right

----------------

If mid > mid+1

Peak exists on left side

Move Left
```

---

## Interview Explanation

### State

```text
Peak element > both neighbours
```

### Task

```text
Find any peak
```

### Observation

```text
Increasing slope

→ peak ahead

Decreasing slope

→ peak behind
```

---

## Recognition Clues

```text
Peak
Mountain
Local Maximum
O(logN)
```

---

## TC / SC

```text
TC = O(logN)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int findPeakElement(int[] nums) {

        int n = nums.length;

        if(n == 1) return 0;

        if(nums[0] > nums[1]) return 0;

        if(nums[n - 1] > nums[n - 2]) return n - 1;

        int s = 0;
        int e = n - 1;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(m > 0 &&
               m < n - 1 &&
               nums[m] > nums[m - 1] &&
               nums[m] > nums[m + 1]){

                return m;
            }

            else if(m < n - 1 &&
                    nums[m] < nums[m + 1]){

                 s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        return -1;
    }
}
```

---

## Quick Revision

```text
mid < mid+1

Move Right

mid > mid+1

Move Left

Think SLOPE
```

---

# Problem 8: Find Square Root of a Number

## Pattern

Binary Search on Answers

---

## Core Idea

Search space:

```text
1 → n
```

Find:

```text
Largest value

x*x <= n
```

---

## Interview Explanation

### State

```text
Answer lies between 1 and n
```

### Task

```text
Find floor(sqrt(n))
```

### Observation

```text
mid² <= n

Possible Answer

Store Answer
Move Right
```

---

## Recognition Clues

```text
Square Root
Floor Value
Answer Space
```

---

## TC / SC

```text
TC = O(logN)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int floorSqrt(int n) {

        if(n == 0) return 0;

        int s = 1;
        int e = n;

        int ans = Integer.MIN_VALUE;

        while(s <= e){

            int m = s + (e - s) / 2;

            if((long)m * m == n){
                  return m;
            }

            else if((long)m * m < n){
                ans = m;
                s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        return ans;
    }
}
```

---

## Quick Revision

```text
mid² <= n

Possible Answer

Move Right

Need Largest Valid Value
```

---

# Problem 9: Find Nth Root of a Number

## Pattern

Binary Search on Answers

---

## Core Idea

Search:

```text
1 → M
```

Find:

```text
x^N = M
```

---

## Interview Explanation

### State

```text
Answer lies between 1 and M
```

### Task

```text
Find integer nth root
```

### Observation

```text
pow(mid,N)

Compare with M
```

---

## Recognition Clues

```text
Nth Root
Power Function
Monotonic Search Space
```

---

## TC / SC

```text
TC = O(logM * N)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int NthRoot(int N, int M) {

        int s = 1;
        int e = M;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(pow(m, N) == M){
                return m;
            }

            else if(pow(m, N) < M){
                s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        return -1;
    }

    public long pow(int x, int N){

        long ans = 1;

        for(int i = 0; i < N; i++){
            ans *= x;
        }

        return ans;
    }
}
```

---

## Quick Revision

```text
mid^N == M

Answer Found

mid^N < M

Move Right

mid^N > M

Move Left
```

---

# Problem 10: Koko Eating Bananas

## Pattern

Binary Search on Answers (First True)

---

## Core Idea

Search Space:

```text
1 → maxPile
```

mid represents:

```text
Bananas Per Hour
```

---

## Interview Explanation

### State

```text
Need minimum eating speed
```

### Task

```text
Find smallest speed
that finishes within h hours
```

### Observation

```text
If speed works

Try smaller speed

Move Left
```

---

## Recognition Clues

```text
Minimum Speed
Minimum Capacity
Minimum Rate
```

---

## TC / SC

```text
TC = O(N log(maxPile))

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int minEatingSpeed(int[] piles, int h) {

        int n = piles.length;

        int max = Integer.MIN_VALUE;

        for(int i = 0; i < n; i++){
            if(piles[i] > max){
                max = piles[i];
            }
        }

        int s = 1;
        int e = max;

        int ans = 0;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(possible(piles, m, h)){
                ans = m;
                e = m - 1;
            }

            else{
                s = m + 1;
            }
        }

        return ans;
    }

    public boolean possible(int[] piles,
                            int possiblee,
                            int hr){

        int n = piles.length;

        int hrsPossible = 0;

        for(int i = 0; i< n; i++){

            hrsPossible += Math.ceil(
                    (double)piles[i]
                  / (double)possiblee
            );
        }

        return hrsPossible <= hr;
    }
}
```

---

## Quick Revision

```text
mid = Speed

Can Finish?

YES

Store Answer
Move Left

FIRST TRUE PATTERN
```

---

# Pattern Summary

```text
SINGLE ELEMENT
→ Pair Property

PEAK ELEMENT
→ Slope Property

SQUARE ROOT
→ Largest Valid Value

NTH ROOT
→ Power Comparison

KOKO
→ First True Binary Search
```

# Pattern 36: Binary Search on Answers (Part 3)

---

# Problem 11: Minimum Days to Make M Bouquets

## Pattern

Binary Search on Answers (First True)

---

## Core Idea

Search Space:

```text
minBloomDay → maxBloomDay
```

mid represents:

```text
Days Allowed
```

---

## Interview Explanation

### State

```text
Each flower blooms on bloomDay[i]
Need m bouquets
Each bouquet needs k adjacent flowers
```

### Task

```text
Find minimum days required
```

### Observation

```text
If bouquets can be formed in mid days

Try smaller days

Move Left
```

---

## Recognition Clues

```text
Minimum Days
Minimum Time
Minimum Capacity
Minimum Rate

=> First True Binary Search
```

---

## TC / SC

```text
TC = O(N log(MaxBloom))

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int minDays(int[] bloomDay, int m, int k) {

        int n = bloomDay.length;

        if((long)m * k > n) return -1;

        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        for(int i = 0; i < n; i++){

            if(bloomDay[i] < min){
                min = bloomDay[i];
            }

            if(bloomDay[i] > max){
                max = bloomDay[i];
            }
        }

        int s = min;
        int e = max;

        int ans = 0;

        while(s <= e){

            int mid = s + (e - s)/ 2;

            if(possible(bloomDay, mid, m, k)){
                ans = mid;
                e = mid - 1;
            }

            else{
                s = mid + 1;
            }
        }

        return ans;
    }

    public boolean possible(int[] bloomDay,
                            int daysPossible,
                            int bouquets,
                            int k){

        int bouquetsFilled = 0;
        int cnt = 0;

        for(int i = 0; i < bloomDay.length; i++){

            if(bloomDay[i] <= daysPossible){
                cnt++;
            }

            else{
                bouquetsFilled += cnt / k;
                cnt = 0;
            }
        }

        bouquetsFilled += cnt / k;

        return bouquetsFilled >= bouquets;
    }
}
```

---

## Quick Revision

```text
mid = Days

Can Make m Bouquets?

YES
Move Left

NO
Move Right
```

---

# Problem 12: Find the Smallest Divisor Given a Threshold

## Pattern

Binary Search on Answers (First True)

---

## Core Idea

Search Space:

```text
1 → max(nums)
```

mid represents:

```text
Divisor
```

---

## Interview Explanation

### State

```text
Need smallest divisor
```

### Task

```text
Sum of ceil(nums[i]/divisor)
must remain <= threshold
```

### Observation

```text
If divisor works

Try smaller divisor

Move Left
```

---

## Recognition Clues

```text
Minimum Divisor
Minimum Speed
Minimum Capacity

=> First True Pattern
```

---

## TC / SC

```text
TC = O(N log(MaxElement))

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int smallestDivisor(int[] nums,
                               int threshold) {

        int max = Integer.MIN_VALUE;

        for(int num : nums){
            max = Math.max(max, num);
        }

        int s = 1;
        int e = max;

        int ans = 0;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(possible(nums, m, threshold)){
                ans = m;
                e = m - 1;
            }

            else{
                s = m + 1;
            }
        }

        return ans;
    }

    public boolean possible(int[] nums,
                            int divisor,
                            int threshold){

        int ans = 0;

        for(int num : nums){

            ans += (int)Math.ceil(
                    (double)num/divisor
                  );
        }

        return ans <= threshold;
    }
}
```

---

## Quick Revision

```text
mid = Divisor

Works?

YES
Move Left

Need Minimum Divisor
```

---

# Problem 13: Capacity To Ship Packages Within D Days

## Pattern

Binary Search on Answers (First True)

---

## Core Idea

Search Space:

```text
max(weights)
        →
sum(weights)
```

mid represents:

```text
Ship Capacity
```

---

## Interview Explanation

### State

```text
Ship packages in order
Need capacity
```

### Task

```text
Find minimum capacity
that ships all packages
within D days
```

### Observation

```text
If capacity works

Try smaller capacity

Move Left
```

---

## Recognition Clues

```text
Minimum Capacity
Minimum Weight
Minimum Load

=> First True
```

---

## TC / SC

```text
TC = O(N log(sum))

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int shipWithinDays(int[] weights,
                              int days) {

       int max = Integer.MIN_VALUE;
       int sum = 0;

       for(int w : weights){

            max = Math.max(max, w);
            sum += w;
       }

       int s = max;
       int e = sum;

       int ans = 0;

       while(s <= e){

            int m = s + (e - s) / 2;

            if(possible(weights, m, days)){
                ans = m;
                e = m - 1;
            }

            else{
                s = m + 1;
            }
       }

       return ans;
    }

    public boolean possible(int[] weights,
                            int packages,
                            int days){

        int day = 1;
        int cntOfPackages = 0;

        for(int i = 0; i < weights.length; i++){

            if(cntOfPackages + weights[i]
                <= packages){

                cntOfPackages += weights[i];
            }

            else{

                day++;
                cntOfPackages = weights[i];
            }
        }

        return day <= days;
    }
}
```

---

## Quick Revision

```text
mid = Capacity

Can Ship?

YES
Move Left

Need Minimum Capacity
```

---

# Problem 14: Kth Missing Positive Number

## Pattern

Binary Search on Missing Count

---

## Core Idea

Missing Numbers till index m:

```text
missing = arr[m] - (m + 1)
```

---

## Interview Explanation

### State

```text
Sorted Positive Array
Some numbers missing
```

### Task

```text
Find kth missing number
```

### Observation

```text
missing(mid)

If less than k

Move Right

Else

Move Left
```

---

## Recognition Clues

```text
Missing Numbers
Sorted Array
Index Formula
```

---

## TC / SC

```text
TC = O(logN)

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int findKthPositive(int[] arr,
                               int k) {

         int n = arr.length;

         int s = 0;
         int e = n - 1;

         while(s <= e){

            int m = s + (e - s) / 2;

            int missing =
                    arr[m] - (m + 1);

            if(missing < k){
                s = m + 1;
            }

            else{
                e = m - 1;
            }
         }

         return s + k;
    }
}
```

---

## Quick Revision

```text
missing(mid)

=
arr[mid] - (mid+1)

Answer

=
low + k
```

---

# Problem 15: Aggressive Cows

## Pattern

Binary Search on Answers (Last True)

---

## Core Idea

Search Space:

```text
1
→
maxDistance
```

mid represents:

```text
Minimum Distance
between cows
```

---

## Interview Explanation

### State

```text
Need maximum minimum distance
```

### Task

```text
Place all cows
while maximizing
minimum distance
```

### Observation

```text
If distance works

Try bigger distance

Move Right
```

---

## Recognition Clues

```text
Maximum Minimum Distance
Largest Possible Value

=> Last True Pattern
```

---

## TC / SC

```text
TC = O(Nlog(MaxDistance))

SC = O(1)
```

---

## Java Code

```java
class Solution {

    public int aggressiveCows(int[] nums,
                              int k) {

        Arrays.sort(nums);

        int n = nums.length;

        int s = 1;
        int e = nums[n - 1] - nums[0];

        int ans = Integer.MIN_VALUE;

        while(s <= e){

            int m = s + (e - s) / 2;

            if(canWePlace(nums, k, m)){
                ans = m;
                s = m + 1;
            }

            else{
                e = m - 1;
            }
        }

        return ans;
    }

    public boolean canWePlace(int[] arr,
                              int cows,
                              int minDist){

        int cowsPlaced = 1;

        int last = arr[0];

        for(int i = 0; i < arr.length; i++){

            if(arr[i] - last >= minDist){

                cowsPlaced++;
                last = arr[i];
            }
        }

        return cowsPlaced >= cows;
    }
}
```

---

## Quick Revision

```text
mid = Distance

Can Place All Cows?

YES
Move Right

Need Maximum Answer

LAST TRUE PATTERN
```

---

# Pattern Summary

```text
BOUQUETS
→ First True

SMALLEST DIVISOR
→ First True

SHIP PACKAGES
→ First True

KTH MISSING
→ Missing Count Formula

AGGRESSIVE COWS
→ Last True
```

# Google Interview Memory Trick

```text
Need MINIMUM Answer?

Move LEFT when possible

Examples:

Koko
Bouquets
Divisor
Ship Packages
Book Allocation

-------------------

Need MAXIMUM Answer?

Move RIGHT when possible

Example:

Aggressive Cows
```

# Pattern 37: Book Allocation + Master Binary Search on Answers Pattern

---

# Problem 16: Book Allocation Problem

## Pattern

Binary Search on Answers (First True)

---

## Core Idea

Search Space:

```text id="lm4gb7"
max(bookPages)
        →
sum(bookPages)
```

mid represents:

```text id="e1g1n4"
Maximum pages
allowed to a student
```

---

## Interview Explanation

### State

```text id="jgg8dg"
Books must be allocated
contiguously

Every student must
receive at least one book
```

### Task

```text id="c07lmj"
Minimize

Maximum pages assigned
to any student
```

---

### Observation

```text id="r9b6al"
If allocation possible
with mid pages

Try smaller maximum

Move Left
```

---

## Recognition Clues

```text id="o1zvzh"
Minimize Maximum

Allocate Resources

Partition Array

Contiguous Allocation

Students
Painters
Workers

=> Binary Search on Answers
```

---

## Why Search Space is

```text id="l8b5pg"
max(bookPages)
        →
sum(bookPages)
```

### Lower Bound

```text id="kvd2od"
At least one student
must take the largest book

So answer can never be
smaller than max(book)
```

### Upper Bound

```text id="k7stot"
One student takes
all books

Maximum pages
=
sum(all books)
```

---

## TC / SC

```text id="v0mkpb"
TC = O(N log(sum))

SC = O(1)
```

---

## Java Code

```java id="o3ck0g"
class Solution {

    public int findPages(int[] nums, int m) {

        int n = nums.length;

        if(m > n){
            return -1;
        }

        int max = Integer.MIN_VALUE;
        int sum = 0;

        for(int i = 0; i < n; i++){

            if(nums[i] > max){
                max = nums[i];
            }

            sum += nums[i];
        }

        int s = max;
        int e = sum;

        int ans = 0;

        while(s <= e){

            int mid = s + (e - s) / 2;

            if(allocationPossible(nums, mid, m)){

                ans = mid;
                e = mid - 1;
            }

            else{
                s = mid + 1;
            }
        }

        return s;
    }

    public boolean allocationPossible(int[] nums,
                                      int maxPossible,
                                      int students){

        int studentsAllocatedBooks = 1;

        int sum = 0;

        for(int i = 0; i < nums.length; i++){

            if(sum + nums[i] <= maxPossible){

                sum += nums[i];
            }

            else{

                studentsAllocatedBooks++;
                sum = nums[i];
            }
        }

        return studentsAllocatedBooks <= students;
    }
}
```

---

## Dry Run

```text id="ywdo3g"
Books

10 20 30 40

Students = 2

Try mid = 60

Student 1

10 + 20 + 30 = 60

Student 2

40

Students Needed = 2

Possible

Move Left
```

---

## Quick Revision

```text id="b7ajcc"
mid

=
Maximum Pages

Possible?

YES

Move Left

Need Minimum Answer
```

---

