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
