# 2. Two Pointer Recursion Pattern

## Core Idea

Use two pointers (`left` and `right`) and move them towards each other after every recursive call.

Applicable when:

* Comparing elements from both ends.
* Swapping elements from both ends.
* Working on the remaining middle portion.

---

# 2.1 Reverse an Array

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

* left
* right

**Task:**

* Reverse subarray from left to right.

**Observation:**

* After placing outer elements in correct positions,
  only the middle part remains.

**Smaller Problem:**

```text
reverse(left + 1, right - 1)
```

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 2.2 Check if String is Palindrome

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

        // Check remaining substring
        return isPalindrome(s, left + 1, right - 1);
    }
}
```

### Interview Explanation

**State:**

* left
* right

**Task:**

* Check whether substring between left and right is palindrome.

**Observation:**

* If outer characters match,
  only inner substring matters.

**Smaller Problem:**

```text
isPalindrome(left + 1, right - 1)
```

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# Two Pointer Recursion Recognition

Whenever you hear:

```text
Compare first and last
Compare ends
Swap ends
Process outer elements first
```

Think:

```text
left++
right--
```

and recurse on the middle part.

---

# Quick Revision Table

| Problem          | State      | Recurrence              | TC   | SC   |
| ---------------- | ---------- | ----------------------- | ---- | ---- |
| Reverse Array    | left,right | reverse(left+1,right-1) | O(N) | O(N) |
| Palindrome Check | left,right | check(left+1,right-1)   | O(N) | O(N) |

---

# 3. Frequency Counting / Hashing Pattern

## Core Idea

Store information about elements while traversing the array.

Most commonly:

```text
Element -> Frequency
```

Hashing allows:

```text
Search  -> O(1)
Insert  -> O(1)
Update  -> O(1)
```

on average.

---

# 3.1 Basic Hashing

### Goal

Store occurrences of elements.

```java
HashMap<Integer, Integer> map = new HashMap<>();

for(int num : arr){
    map.put(num, map.getOrDefault(num, 0) + 1);
}
```

### Interview Explanation

**State:**

* map[element] = frequency

**Task:**

* Record how many times each element appears.

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 3.2 Counting Frequencies of Array Elements

```java
class Solution {

    public HashMap<Integer,Integer> countFreq(int[] arr){

        HashMap<Integer,Integer> map = new HashMap<>();

        for(int num : arr){
            map.put(num, map.getOrDefault(num,0) + 1);
        }

        return map;
    }
}
```

### Interview Explanation

**Observation:**

When an element appears again:

```text
frequency++
```

HashMap helps us update frequency in O(1).

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# 3.3 Highest Occurring Element in an Array

```java
class Solution {

    public int highestOccurring(int[] arr){

        HashMap<Integer,Integer> map = new HashMap<>();

        for(int num : arr){
            map.put(num, map.getOrDefault(num,0) + 1);
        }

        int maxFreq = 0;
        int ans = -1;

        for(int key : map.keySet()){

            if(map.get(key) > maxFreq){
                maxFreq = map.get(key);
                ans = key;
            }
        }

        return ans;
    }
}
```

### Interview Explanation

### Step 1

Build frequency table.

```text
Element -> Frequency
```

### Step 2

Find element with maximum frequency.

### Complexity

```text
TC = O(N)
SC = O(N)
```

---

# Hashing Pattern Recognition

Whenever you hear:

```text
Count frequency
Find duplicates
Most frequent element
Least frequent element
Occurrences
Track counts
```

Think:

```java
HashMap<Element, Frequency>
```

---

# Quick Revision Table

| Problem                   | Data Structure | Idea                   | TC   | SC   |
| ------------------------- | -------------- | ---------------------- | ---- | ---- |
| Basic Hashing             | HashMap        | Store frequency        | O(N) | O(N) |
| Count Frequencies         | HashMap        | Frequency table        | O(N) | O(N) |
| Highest Occurring Element | HashMap        | Frequency + max search | O(N) | O(N) |

---

# 4. Selection Sort Pattern

## Core Idea

For every position:

```text
Find smallest element
Place it at correct position
```

After every iteration:

```text
One element reaches its final position.
```

---

# Selection Sort

```java
class Solution {

    public void selectionSort(int[] arr) {

        int n = arr.length;

        for(int i = 0; i < n - 1; i++){

            int minIndex = i;

            for(int j = i + 1; j < n; j++){

                if(arr[j] < arr[minIndex]){
                    minIndex = j;
                }
            }

            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
}
```

### Interview Explanation

### State

```text
i = current position to fill
```

### Task

Find smallest element in:

```text
[i ... n-1]
```

and place it at index `i`.

### Observation

After iteration 1:

```text
Smallest element fixed.
```

After iteration 2:

```text
Second smallest fixed.
```

After iteration k:

```text
First k elements are sorted.
```

---

### Example

```text
4 2 1 5 3
```

Pass 1

```text
Find min = 1

1 2 4 5 3
```

Pass 2

```text
Find min = 2

1 2 4 5 3
```

Pass 3

```text
Find min = 3

1 2 3 5 4
```

Pass 4

```text
Find min = 4

1 2 3 4 5
```

---

### Complexity

### Time Complexity

Outer loop:

```text
N-1
```

Inner loop:

```text
N-1 + N-2 + N-3 + ...
```

Total:

```text
O(N²)
```

### Space Complexity

```text
O(1)
```

In-place sorting.

---

# Selection Sort Recognition

Whenever you hear:

```text
Repeatedly choose smallest element
Repeatedly choose largest element
Place selected element at correct position
```

Think:

```text
Selection Sort
```

---

# Quick Revision Table

| Algorithm      | Idea                               | Best TC | Avg TC | Worst TC | SC   |
| -------------- | ---------------------------------- | ------- | ------ | -------- | ---- |
| Selection Sort | Select minimum and place correctly | O(N²)   | O(N²)  | O(N²)    | O(1) |

----

# 5. Bubble Sort Pattern

## Core Idea

Repeatedly compare adjacent elements and swap if they are in the wrong order.

After every pass:

```text
Largest element bubbles to the end.
```

---

# 5.1 Bubble Sort

```java
class Solution {

    public void bubbleSort(int[] arr) {

        int n = arr.length;

        for(int i = 0; i < n - 1; i++) {

            boolean swapped = false;

            for(int j = 0; j < n - i - 1; j++) {

                if(arr[j] > arr[j + 1]) {

                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;

                    swapped = true;
                }
            }

            if(!swapped) break;
        }
    }
}
```

### Interview Explanation

**State**

```text
i = current pass
```

**Observation**

After Pass 1:

```text
Largest element reaches last position.
```

After Pass 2:

```text
Second largest reaches second last position.
```

### Complexity

| Case    | TC    |
| ------- | ----- |
| Best    | O(N)  |
| Average | O(N²) |
| Worst   | O(N²) |

```text
SC = O(1)
```

---

# Bubble Sort Recognition

```text
Repeated adjacent swaps
Largest element moves right
```

Think:

```text
Bubble Sort
```

---

# 5.2 Recursive Bubble Sort

## Core Idea

One recursive call handles one pass.

```java
class Solution {

    public void bubbleSort(int[] arr) {
        bubble(arr, arr.length);
    }

    private void bubble(int[] arr, int n) {

        if(n == 1) return;

        for(int i = 0; i < n - 1; i++) {

            if(arr[i] > arr[i + 1]) {

                int temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;
            }
        }

        bubble(arr, n - 1);
    }
}
```

### Interview Explanation

**State**

```text
n = size of unsorted portion
```

**Observation**

One pass places largest element correctly.

Now sort remaining:

```text
0 ... n-2
```

### Complexity

```text
TC = O(N²)
SC = O(N)
```

---

# Quick Revision Table

| Algorithm             | Idea                   | TC    | SC   |
| --------------------- | ---------------------- | ----- | ---- |
| Bubble Sort           | Adjacent swaps         | O(N²) | O(1) |
| Recursive Bubble Sort | One pass per recursion | O(N²) | O(N) |

---

# 6. Insertion Sort Pattern

## Core Idea

Maintain a sorted portion on the left.

Insert current element into its correct position.

---

# 6.1 Insertion Sort

```java
class Solution {

    public void insertionSort(int[] arr) {

        int n = arr.length;

        for(int i = 1; i < n; i++) {

            int current = arr[i];
            int j = i - 1;

            while(j >= 0 && arr[j] > current) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = current;
        }
    }
}
```

### Interview Explanation

**State**

```text
0 ... i-1 is already sorted
```

**Task**

Insert:

```text
arr[i]
```

into its correct position.

### Example

```text
5 3 4 1
```

Insert 3

```text
3 5 4 1
```

Insert 4

```text
3 4 5 1
```

Insert 1

```text
1 3 4 5
```

### Complexity

| Case    | TC    |
| ------- | ----- |
| Best    | O(N)  |
| Average | O(N²) |
| Worst   | O(N²) |

```text
SC = O(1)
```

---

# Insertion Sort Recognition

Whenever you hear:

```text
Maintain sorted portion
Insert element into sorted array
Card sorting
```

Think:

```text
Insertion Sort
```

---

# 6.2 Recursive Insertion Sort

```java
class Solution {

    public void insertionSort(int[] arr) {
        sort(arr, arr.length);
    }

    private void sort(int[] arr, int n) {

        if(n <= 1) return;

        sort(arr, n - 1);

        int last = arr[n - 1];
        int j = n - 2;

        while(j >= 0 && arr[j] > last) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = last;
    }
}
```

### Interview Explanation

**State**

```text
First n elements
```

**Observation**

Recursively sort:

```text
0 ... n-2
```

Then insert:

```text
arr[n-1]
```

into correct position.

### Complexity

```text
TC = O(N²)
SC = O(N)
```

---

# Quick Revision Table

| Algorithm                | Idea                         | TC    | SC   |
| ------------------------ | ---------------------------- | ----- | ---- |
| Insertion Sort           | Insert in sorted portion     | O(N²) | O(1) |
| Recursive Insertion Sort | Recursively sort then insert | O(N²) | O(N) |

---

# 7. Merge Sort / Divide & Conquer Pattern

## Core Idea

```text
Divide
↓
Solve smaller problems
↓
Merge answers
```

---

# 7.1 Merge Sort

```java
class Solution {

    public void mergeSort(int[] arr, int low, int high) {

        if(low >= high) return;

        int mid = low + (high - low) / 2;

        mergeSort(arr, low, mid);
        mergeSort(arr, mid + 1, high);

        merge(arr, low, mid, high);
    }
}
```

### Interview Explanation

**State**

```text
Sort subarray [low...high]
```

**Observation**

Sort:

```text
Left Half
Right Half
```

Then combine.

### Complexity

```text
TC = O(N log N)
SC = O(N)
```

---

# Merge Sort Recognition

Whenever you hear:

```text
Divide array into halves
Sort halves independently
Merge results
```

Think:

```text
Merge Sort
```

---

# 7.2 Count Inversions

## Problem

Count pairs:

```text
i < j
arr[i] > arr[j]
```

---

## Optimal Idea

While merging:

```text
Left half sorted
Right half sorted
```

If:

```text
left[i] > right[j]
```

Then:

```text
All remaining left elements
form inversions.
```

### Formula

```text
count += (mid - i + 1)
```

### Interview Explanation

Suppose:

```text
2 4 5
1 3
```

At:

```text
2 > 1
```

Then:

```text
2,4,5 all form inversions with 1
```

Count:

```text
3
```

immediately.

### Complexity

```text
TC = O(N log N)
SC = O(N)
```

---

# Count Inversions Recognition

Whenever you hear:

```text
Count pairs
i < j
arr[i] > arr[j]
```

Think:

```text
Merge Sort Modification
```

---

# 7.3 Reverse Pairs

## Problem

Count pairs:

```text
i < j
arr[i] > 2 * arr[j]
```

---

## Optimal Idea

Before merging:

Use two pointers.

For every left element:

```text
Find how many right elements satisfy

arr[i] > 2*arr[j]
```

### Interview Explanation

Since both halves are sorted:

```text
Pointer never moves backward.
```

Thus counting becomes linear.

After counting:

```text
Perform normal merge.
```

### Complexity

```text
TC = O(N log N)
SC = O(N)
```

---

# Reverse Pair Recognition

Whenever you hear:

```text
Count pairs
i < j
Condition involving both sides
```

Especially:

```text
arr[i] > k * arr[j]
```

Think:

```text
Modified Merge Sort
```

---

# Quick Revision Table

| Problem          | Pattern             | Idea                  | TC         | SC   |
| ---------------- | ------------------- | --------------------- | ---------- | ---- |
| Merge Sort       | Divide & Conquer    | Divide → Sort → Merge | O(N log N) | O(N) |
| Count Inversions | Modified Merge Sort | Count during merge    | O(N log N) | O(N) |
| Reverse Pairs    | Modified Merge Sort | Count before merge    | O(N log N) | O(N) |

---

# Divide & Conquer Recognition

Whenever you hear:

```text
Split problem into smaller independent parts
Solve each part
Combine answers
```

Think:

```text
Divide & Conquer
```

Most common examples:

```text
Merge Sort
Quick Sort
Count Inversions
Reverse Pairs
Binary Search
```
---

# 8. Quick Sort / Partition Pattern

## Core Idea

Choose a pivot and place it in its correct sorted position.

After partitioning:

```text
Left Side  -> Smaller than pivot
Pivot      -> Correct position
Right Side -> Greater than pivot
```

Then recursively sort left and right parts.

---

# 8.1 Quick Sort

```java
class Solution {

    public void quickSort(int[] arr, int low, int high) {

        if(low < high){

            int pIndex = partition(arr, low, high);

            quickSort(arr, low, pIndex - 1);
            quickSort(arr, pIndex + 1, high);
        }
    }
}
```

### Interview Explanation

### State

```text
Sort subarray [low...high]
```

### Observation

If pivot reaches its final position:

```text
Everything left is smaller
Everything right is larger
```

Now sort both halves independently.

### Complexity

| Case    | TC         |
| ------- | ---------- |
| Best    | O(N log N) |
| Average | O(N log N) |
| Worst   | O(N²)      |

```text
SC = O(log N) Average
SC = O(N) Worst
```

---

# Partition Algorithm (Hoare Partition)

```java
public int partition(int[] arr, int low, int high){

    int pivot = arr[low];

    int i = low;
    int j = high;

    while(i < j){

        while(arr[i] <= pivot && i <= high - 1)
            i++;

        while(arr[j] > pivot && j >= low + 1)
            j--;

        if(i < j){
            swap(arr, i, j);
        }
    }

    swap(arr, low, j);

    return j;
}
```

---

## Interview Explanation

### State

```text
pivot = arr[low]
```

### Goal

Place pivot in its correct position.

### Observation

Move:

```text
i -> first element > pivot
j -> first element <= pivot
```

Swap them.

When:

```text
i >= j
```

Pivot belongs at:

```text
index j
```

### Complexity

```text
Partition TC = O(N)
Partition SC = O(1)
```

---

# Quick Sort Recognition

Whenever you hear:

```text
Pivot
Partition
Sort around pivot
```

Think:

```text
Quick Sort
```

---

# Quick Revision Table

| Algorithm  | Idea                   | Avg TC     | Worst TC | SC       |
| ---------- | ---------------------- | ---------- | -------- | -------- |
| Quick Sort | Partition around pivot | O(N log N) | O(N²)    | O(log N) |

---

# 9. Linear Traversal Pattern

## Core Idea

Process every element exactly once.

Usually maintain some variable while traversing.

```text
for each element
    update answer
```

---

# 9.1 Largest Element

```java
class Solution {

    public int largestElement(int[] arr){

        int max = arr[0];

        for(int num : arr){
            max = Math.max(max, num);
        }

        return max;
    }
}
```

### Interview Explanation

### State

```text
max = largest element seen so far
```

### Observation

Every new element gets one chance to become maximum.

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 9.2 Check if Array is Sorted

```java
class Solution {

    public boolean isSorted(int[] arr){

        for(int i = 1; i < arr.length; i++){

            if(arr[i] < arr[i - 1])
                return false;
        }

        return true;
    }
}
```

### Interview Explanation

### Observation

For sorted array:

```text
arr[i] >= arr[i-1]
```

must hold for every index.

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 9.3 Linear Search

```java
class Solution {

    public int search(int[] arr, int target){

        for(int i = 0; i < arr.length; i++){

            if(arr[i] == target)
                return i;
        }

        return -1;
    }
}
```

### Interview Explanation

### Observation

Check every element until target is found.

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 9.4 Maximum Consecutive Ones

```java
class Solution {

    public int findMaxConsecutiveOnes(int[] nums){

        int cnt = 0;
        int maxCnt = 0;

        for(int num : nums){

            if(num == 1){

                cnt++;
                maxCnt = Math.max(maxCnt, cnt);
            }
            else{
                cnt = 0;
            }
        }

        return maxCnt;
    }
}
```

### Interview Explanation

### State

```text
cnt = current streak of ones
maxCnt = best streak seen so far
```

### Observation

Whenever:

```text
1 -> extend streak
0 -> break streak
```

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# Linear Traversal Recognition

Whenever you hear:

```text
Find max
Find min
Search element
Check property
Count occurrences
```

Think:

```text
Single traversal
```

---

# Quick Revision Table

| Problem                  | State            | TC   | SC   |
| ------------------------ | ---------------- | ---- | ---- |
| Largest Element          | max              | O(N) | O(1) |
| Check Sorted             | compare adjacent | O(N) | O(1) |
| Linear Search            | search target    | O(N) | O(1) |
| Maximum Consecutive Ones | cnt,maxCnt       | O(N) | O(1) |

---

# 10. Running Maximum / Running Minimum Pattern

## Core Idea

Maintain the best value seen so far while traversing.

```text
Running Maximum
Running Minimum
```

This avoids nested loops.

---

# 10.1 Largest Element

```java
int max = arr[0];

for(int num : arr){
    max = Math.max(max, num);
}
```

### State

```text
max = largest seen so far
```

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 10.2 Second Largest Element

```java
class Solution {

    public int secondLargest(int[] arr){

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for(int num : arr){

            if(num > largest){

                secondLargest = largest;
                largest = num;
            }
            else if(num > secondLargest && num != largest){

                secondLargest = num;
            }
        }

        return secondLargest;
    }
}
```

### Interview Explanation

### State

```text
largest
secondLargest
```

### Observation

When new largest appears:

```text
Old largest becomes second largest.
```

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 10.3 Stock Buy and Sell

## Problem

Maximize:

```text
sellPrice - buyPrice
```

---

```java
class Solution {

    public int maxProfit(int[] prices){

        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for(int price : prices){

            minPrice = Math.min(minPrice, price);

            maxProfit =
                Math.max(maxProfit, price - minPrice);
        }

        return maxProfit;
    }
}
```

### Interview Explanation

### State

```text
minPrice = lowest price seen so far
```

### Observation

Every day:

```text
Current Profit =
Current Price - Best Buy Price
```

Update answer.

### Complexity

```text
TC = O(N)
SC = O(1)
```

---

# 10.4 Leaders in an Array

## Problem

Leader:

```text
Element greater than all elements on right.
```

---

```java
class Solution {

    public List<Integer> leaders(int[] arr){

        List<Integer> ans = new ArrayList<>();

        int maxRight = Integer.MIN_VALUE;

        for(int i = arr.length - 1; i >= 0; i--){

            if(arr[i] > maxRight){

                ans.add(arr[i]);
                maxRight = arr[i];
            }
        }

        Collections.reverse(ans);

        return ans;
    }
}
```

### Interview Explanation

### State

```text
maxRight = largest element seen on right
```

### Observation

Traverse from right.

If:

```text
arr[i] > maxRight
```

then:

```text
arr[i]
```

is a leader.

### Complexity

```text
TC = O(N)
SC = O(N)
```

(Result list excluded → auxiliary SC = O(1))

---

# Running Maximum / Minimum Recognition

Whenever you hear:

```text
Best so far
Largest so far
Smallest so far
Maximum profit
Maximum on right
```

Think:

```text
Running Max / Running Min
```

---

# Quick Revision Table

| Problem          | State                 | Idea              | TC   | SC   |
| ---------------- | --------------------- | ----------------- | ---- | ---- |
| Largest Element  | max                   | Running maximum   | O(N) | O(1) |
| Second Largest   | largest,secondLargest | Track top 2       | O(N) | O(1) |
| Stock Buy & Sell | minPrice              | Running minimum   | O(N) | O(1) |
| Leaders in Array | maxRight              | Right-to-left max | O(N) | O(N) |

---

# 11. Two Variable Tracking Pattern

## Core Idea

Instead of tracking only one value (maximum/minimum), track multiple related values while traversing the array.

Examples:

* Largest + Second Largest
* Smallest + Second Smallest
* Min Price + Max Profit

---

## Interview Explanation

### State

```text
largest
secondLargest
```

### Task

For every element, decide whether it becomes:

* Largest
* Second Largest
* Ignored

### Observation

When a new largest element arrives:

```text
old largest
becomes
second largest
```

---

## Recognition Clues

Questions containing:

```text
Second Largest
Second Smallest
Top 2 values
Track best and second best
```

Think:

```text
Maintain multiple answers simultaneously
```

---

## Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(N)  |
| Space  | O(1)  |

---

## Quick Revision

| Problem         | State Variables          |
| --------------- | ------------------------ |
| Second Largest  | largest, secondLargest   |
| Second Smallest | smallest, secondSmallest |
| Stock Buy Sell  | minPrice, maxProfit      |

---

## Java Code

```java
int largest = Integer.MIN_VALUE;
int secondLargest = Integer.MIN_VALUE;

for(int num : arr){

    if(num > largest){
        secondLargest = largest;
        largest = num;
    }
    else if(num > secondLargest && num != largest){
        secondLargest = num;
    }
}
```

---

# 12. Two Pointer Array Pattern

## Problems

* Remove Duplicates From Sorted Array
* Move Zeroes To End

---

## A) Remove Duplicates From Sorted Array

### Core Idea

Use:

```text
i -> last unique element
j -> current element
```

Keep only unique values at the beginning.

### Interview Explanation

#### State

```text
i = position of last unique element
```

#### Task

Find next unique element.

#### Observation

If:

```text
arr[j] != arr[i]
```

Then:

```text
i++
arr[i] = arr[j]
```

### Recognition Clues

```text
Sorted Array
Remove Duplicates
Unique Elements
In-place
```

Think:

```text
Slow Pointer + Fast Pointer
```

### Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(N)  |
| Space  | O(1)  |

### Java Code

```java
int i = 0;

for(int j = 1; j < arr.length; j++){

    if(arr[j] != arr[i]){
        i++;
        arr[i] = arr[j];
    }
}

return i + 1;
```

---

## B) Move Zeroes To End

### Core Idea

Put every non-zero element in its correct position.

### Interview Explanation

#### State

```text
j = first zero position
```

#### Task

Whenever non-zero appears after zero:

```text
swap
```

#### Observation

All non-zero elements must remain in the same order.

### Recognition Clues

```text
Move Zeroes
Stable Rearrangement
Push all X to end
In-place
```

Think:

```text
Two Pointers
```

### Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(N)  |
| Space  | O(1)  |

### Java Code

```java
int j = -1;

for(int i = 0; i < n; i++){
    if(arr[i] == 0){
        j = i;
        break;
    }
}

if(j == -1) return;

for(int i = j + 1; i < n; i++){

    if(arr[i] != 0){

        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;

        j++;
    }
}
```

---

# 13. Array Rotation Pattern

## Problems

* Left Rotate Array by One
* Left Rotate Array by K Places

---

## A) Left Rotate Array By One

### Core Idea

Save first element.

Shift everything left.

Place first element at the end.

### Recognition Clues

```text
Rotate
Shift
Circular Movement
```

### Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(N)  |
| Space  | O(1)  |

### Java Code

```java
int temp = arr[0];

for(int i = 1; i < n; i++){
    arr[i - 1] = arr[i];
}

arr[n - 1] = temp;
```

---

## B) Left Rotate Array By K Places

### Core Idea

Use Reversal Algorithm.

```text
Reverse(0, k-1)
Reverse(k, n-1)
Reverse(0, n-1)
```

### Interview Explanation

#### Observation

After reversing the two parts separately:

```text
Both parts are internally correct.
```

The final reversal joins them into the rotated order.

### Recognition Clues

```text
Rotate Array
Rotate by K
In-place Rotation
```

Think:

```text
Reversal Algorithm
```

### Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(N)  |
| Space  | O(1)  |

### Java Code

```java
k = k % n;

reverse(arr, 0, k - 1);
reverse(arr, k, n - 1);
reverse(arr, 0, n - 1);
```

---

# 14. Merge Two Sorted Arrays Pattern

## Problems

* Union of Two Sorted Arrays
* Merge Two Sorted Arrays Without Extra Space

---

## A) Union of Two Sorted Arrays

### Core Idea

Use two pointers.

Always take the smaller element.

Avoid duplicates.

### Interview Explanation

#### State

```text
i -> arr1
j -> arr2
```

#### Observation

Since arrays are sorted:

```text
Smaller element must come first.
```

### Recognition Clues

```text
Union
Sorted Arrays
Merge While Removing Duplicates
```

Think:

```text
Two Pointer Merge
```

### Complexity

| Metric | Value    |
| ------ | -------- |
| Time   | O(N + M) |
| Space  | O(N + M) |

---

## B) Merge Two Sorted Arrays Without Extra Space

### Core Idea

Use the Gap Method (Shell Sort Idea).

### Interview Explanation

#### State

```text
gap
left
right
```

#### Task

Compare elements gap distance apart.

If out of order:

```text
swap
```

#### Observation

Large elements move right.

Small elements move left.

Eventually:

```text
gap = 1
```

and arrays become completely merged.

### Recognition Clues

```text
Merge Without Extra Space
No Extra Array
In-place Merge
```

Think:

```text
Gap Method
```

### Complexity

| Metric | Value                 |
| ------ | --------------------- |
| Time   | O((N + M) log(N + M)) |
| Space  | O(1)                  |

---

## Quick Revision

| Problem                   | Pattern           |
| ------------------------- | ----------------- |
| Union of Sorted Arrays    | Two Pointer Merge |
| Merge Without Extra Space | Gap Method        |

---

# Pattern Summary

| Problem                   | Pattern               |
| ------------------------- | --------------------- |
| Second Largest            | Two Variable Tracking |
| Remove Duplicates         | Slow/Fast Pointer     |
| Move Zeroes               | Two Pointer Swap      |
| Left Rotate By One        | Shift                 |
| Left Rotate By K          | Reversal Algorithm    |
| Union Sorted Arrays       | Two Pointer Merge     |
| Merge Without Extra Space | Gap Method            |

---

# 15. Missing Number Pattern

## Problems

* Find Missing Number
* Find Repeating and Missing Number

---

# A) Find Missing Number

## Core Idea

Numbers should be present from:

```text
0 → N
```

One number is missing.

Find the difference between expected and actual values.

---

## Interview Explanation

### State

```text
Expected Sum
Actual Sum
```

### Task

Find the missing number.

### Observation

Expected Sum:

```text
N * (N + 1) / 2
```

Actual Sum:

```text
Sum of Array
```

Difference gives the missing number.

---

## Recognition Clues

```text
0 to N
1 number missing
No duplicates
```

Think:

```text
Expected - Actual
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int missingNumber(int[] nums) {

    int n = nums.length;

    int expected = n * (n + 1) / 2;

    int actual = 0;

    for(int num : nums){
        actual += num;
    }

    return expected - actual;
}
```

---

# B) Find Repeating And Missing Number

## Core Idea

One number occurs twice.

One number never appears.

---

## Interview Explanation

### State

```text
Repeating Number = X
Missing Number = Y
```

### Observation

Using:

```text
X - Y
```

and

```text
X² - Y²
```

We get two equations.

Solve them to obtain X and Y.

---

## Recognition Clues

```text
One repeated
One missing
1 to N
```

Think:

```text
Maths Equations
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int[] findMissingAndRepeatedValues(int[][] grid) {

    long n = grid.length;
    long N = n * n;

    long SN = N * (N + 1) / 2;
    long S2N = N * (N + 1) * (2 * N + 1) / 6;

    long S = 0;
    long S2 = 0;

    for(int[] row : grid){

        for(int num : row){

            S += num;
            S2 += (long)num * num;
        }
    }

    long val1 = S - SN;
    long val2 = (S2 - S2N) / val1;

    long repeating = (val1 + val2) / 2;
    long missing = repeating - val1;

    return new int[]{
        (int)repeating,
        (int)missing
    };
}
```

---

# 16. XOR Pattern

## Problems

* Single Number
* Count Subarrays With XOR K

---

# A) Single Number

## Core Idea

XOR properties:

```text
A ^ A = 0
A ^ 0 = A
```

Duplicate numbers cancel each other.

---

## Interview Explanation

### State

```text
xor = 0
```

### Task

XOR every element.

### Observation

All pairs become zero.

Only unique element survives.

---

## Recognition Clues

```text
Appears once
Others appear twice
```

Think:

```text
XOR Cancellation
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int singleNumber(int[] nums) {

    int xor = 0;

    for(int num : nums){
        xor ^= num;
    }

    return xor;
}
```

---

# B) Count Subarrays With XOR K

## Core Idea

Store prefix XOR.

---

## Interview Explanation

### State

```text
prefixXor
HashMap
```

### Observation

If:

```text
prefixXor ^ oldPrefix = K
```

Then:

```text
oldPrefix = prefixXor ^ K
```

Count all such prefixes.

---

## Recognition Clues

```text
Count Subarrays
Target XOR
```

Think:

```text
Prefix XOR + HashMap
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(N)  |

---

## Java Code

```java
public int subarraysWithXorK(int[] nums, int k) {

    HashMap<Integer,Integer> map = new HashMap<>();

    map.put(0,1);

    int xor = 0;
    int count = 0;

    for(int num : nums){

        xor ^= num;

        count += map.getOrDefault(xor ^ k, 0);

        map.put(
            xor,
            map.getOrDefault(xor,0) + 1
        );
    }

    return count;
}
```

---

# 17. Sliding Window Pattern

## Problem

Longest Subarray With Sum K (Positive Numbers)

---

## Core Idea

Maintain a window.

Expand if sum is small.

Shrink if sum becomes large.

---

## Interview Explanation

### State

```text
left
right
sum
```

### Observation

Positive numbers guarantee:

```text
Add element
⇒ Sum increases

Remove element
⇒ Sum decreases
```

Therefore window movement is valid.

---

## Recognition Clues

```text
Positive Numbers
Longest Subarray
Target Sum
```

Think:

```text
Sliding Window
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int longestSubarray(int[] arr, int k) {

    int left = 0;
    int sum = 0;

    int maxLen = 0;

    for(int right = 0; right < arr.length; right++){

        sum += arr[right];

        while(sum > k){

            sum -= arr[left];
            left++;
        }

        if(sum == k){

            maxLen = Math.max(
                maxLen,
                right - left + 1
            );
        }
    }

    return maxLen;
}
```

---

# 18. Prefix Sum + HashMap Pattern

## Problems

* Longest Subarray With Sum K
* Count Subarrays With Sum K
* Largest Subarray With Sum 0

---

## Core Idea

Instead of checking every subarray:

```text
Store Prefix Information
```

Use:

```text
HashMap
```

for O(1) lookup.

---

# A) Longest Subarray With Sum K

## Interview Explanation

### State

```text
prefixSum
HashMap
```

### Observation

If:

```text
currentPrefix - oldPrefix = K
```

Then:

```text
oldPrefix = currentPrefix - K
```

Store first occurrence only.

Earlier index gives longer subarray.

---

## Recognition Clues

```text
Longest Subarray
Negatives Present
Sum K
```

Think:

```text
Prefix Sum + First Occurrence
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(N)  |

---

## Java Code

```java
public int longestSubarray(int[] nums, int k) {

    HashMap<Long,Integer> map = new HashMap<>();

    long sum = 0;

    int maxLen = 0;

    for(int i = 0; i < nums.length; i++){

        sum += nums[i];

        if(sum == k){
            maxLen = i + 1;
        }

        long rem = sum - k;

        if(map.containsKey(rem)){

            maxLen = Math.max(
                maxLen,
                i - map.get(rem)
            );
        }

        if(!map.containsKey(sum)){
            map.put(sum,i);
        }
    }

    return maxLen;
}
```

---

# B) Count Subarrays With Sum K

## Interview Explanation

### State

```text
prefixSum
Frequency Map
```

### Observation

Required Prefix:

```text
currentSum - K
```

Every occurrence contributes.

---

## Recognition Clues

```text
Count Subarrays
Negatives Present
Sum K
```

Think:

```text
Prefix Sum Frequency Map
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(N)  |

---

## Java Code

```java
public int subarraySum(int[] nums, int k) {

    HashMap<Integer,Integer> map = new HashMap<>();

    map.put(0,1);

    int sum = 0;
    int count = 0;

    for(int num : nums){

        sum += num;

        count += map.getOrDefault(sum - k, 0);

        map.put(
            sum,
            map.getOrDefault(sum,0) + 1
        );
    }

    return count;
}
```

---

# C) Largest Subarray With Sum 0

## Core Idea

If the same prefix sum appears twice:

```text
prefix[j] - prefix[i] = 0
```

Subarray sum becomes zero.

---

## Interview Explanation

### State

```text
prefixSum
HashMap
```

### Observation

Store first occurrence only.

This gives maximum length.

---

## Recognition Clues

```text
Largest Subarray
Sum 0
Negative Numbers Allowed
```

Think:

```text
Repeated Prefix Sum
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(N)  |

---

## Java Code

```java
public int maxLen(int[] arr) {

    HashMap<Long,Integer> map = new HashMap<>();

    long sum = 0;

    int maxLen = 0;

    for(int i = 0; i < arr.length; i++){

        sum += arr[i];

        if(sum == 0){
            maxLen = i + 1;
        }

        if(map.containsKey(sum)){

            maxLen = Math.max(
                maxLen,
                i - map.get(sum)
            );
        }
        else{

            map.put(sum,i);
        }
    }

    return maxLen;
}
```

---

# Pattern Summary

| Problem                      | Pattern                  |
| ---------------------------- | ------------------------ |
| Missing Number               | Sum / XOR                |
| Repeating Missing Number     | Maths                    |
| Single Number                | XOR                      |
| Count XOR K                  | Prefix XOR + HashMap     |
| Longest Sum K (Positive)     | Sliding Window           |
| Longest Sum K (Any Integers) | Prefix Sum + HashMap     |
| Count Sum K                  | Prefix Sum Frequency Map |
| Largest Sum 0                | Repeated Prefix Sum      |

---

# 19. Two Sum / Complement Pattern

## Problems

* Two Sum

---

# A) Two Sum

## Core Idea

Instead of checking every pair:

```text
arr[i] + arr[j] = target
```

For every element, find its complement.

```text
complement = target - currentElement
```

Store previously seen elements in a HashMap.

---

## Interview Explanation

### State

```text
currentElement
complement
HashMap
```

### Task

Find two numbers whose sum equals target.

### Observation

If:

```text
a + b = target
```

Then:

```text
b = target - a
```

So while traversing, check whether:

```text
target - currentElement
```

already exists.

---

## Recognition Clues

```text
Pair Sum
Target Sum
Find Two Numbers
Indices Required
```

Think:

```text
Complement Lookup
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(N)  |

---

## Java Code

```java
public int[] twoSum(int[] nums, int target) {

    HashMap<Integer,Integer> map =
        new HashMap<>();

    for(int i = 0; i < nums.length; i++){

        int complement =
            target - nums[i];

        if(map.containsKey(complement)){

            return new int[]{
                map.get(complement),
                i
            };
        }

        map.put(nums[i], i);
    }

    return new int[]{-1,-1};
}
```

---

# 20. Dutch National Flag Pattern

## Problem

* Sort an Array of 0's, 1's and 2's

---

## Core Idea

Maintain three regions.

```text
0's Region
1's Region
2's Region
```

Use:

```text
low
mid
high
```

---

## Interview Explanation

### State

```text
low
mid
high
```

### Regions

```text
0 → low-1     => 0's

low → mid-1   => 1's

mid → high    => Unknown

high+1 → end  => 2's
```

### Task

Process unknown region.

### Observation

If:

```text
arr[mid] == 0
```

Move it left.

If:

```text
arr[mid] == 1
```

Keep it in middle.

If:

```text
arr[mid] == 2
```

Move it right.

---

## Recognition Clues

```text
0 1 2
Three Categories
Sort Colors
Three-way Partition
```

Think:

```text
Dutch National Flag
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public void sortColors(int[] nums) {

    int low = 0;
    int mid = 0;
    int high = nums.length - 1;

    while(mid <= high){

        if(nums[mid] == 0){

            swap(nums, low, mid);

            low++;
            mid++;
        }

        else if(nums[mid] == 1){

            mid++;
        }

        else{

            swap(nums, mid, high);

            high--;
        }
    }
}

private void swap(
    int[] arr,
    int i,
    int j
){

    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

---

# 21. Boyer-Moore Voting Algorithm Pattern

## Problems

* Majority Element-I
* Majority Element-II

---

# A) Majority Element-I

## Problem

Find element appearing:

```text
> N/2 times
```

---

## Core Idea

Majority element survives all cancellations.

---

## Interview Explanation

### State

```text
candidate
count
```

### Observation

Different elements cancel each other.

Majority element appears more than all others combined.

Hence it survives.

---

## Example

```text
2 2 1 1 1 2 2
```

Cancellation:

```text
2 vs 1

2 survives
```

---

## Recognition Clues

```text
Majority Element
More than N/2
```

Think:

```text
Boyer Moore Voting
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int majorityElement(int[] nums) {

    int candidate = 0;
    int count = 0;

    for(int num : nums){

        if(count == 0){

            candidate = num;
        }

        if(num == candidate){

            count++;
        }
        else{

            count--;
        }
    }

    return candidate;
}
```

---

# B) Majority Element-II

## Problem

Find all elements appearing:

```text
> N/3 times
```

At most:

```text
2 elements
```

can satisfy this condition.

---

## Core Idea

Track:

```text
candidate1
candidate2

count1
count2
```

---

## Interview Explanation

### Observation

For N/3 majority:

```text
Maximum 2 answers possible
```

Therefore track two candidates.

Cancel remaining elements.

Verify at the end.

---

## Recognition Clues

```text
More than N/3
Majority Element II
```

Think:

```text
Extended Boyer Moore
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public List<Integer> majorityElement(
    int[] nums
){

    int candidate1 = 0;
    int candidate2 = 0;

    int count1 = 0;
    int count2 = 0;

    for(int num : nums){

        if(candidate1 == num){

            count1++;
        }

        else if(candidate2 == num){

            count2++;
        }

        else if(count1 == 0){

            candidate1 = num;
            count1 = 1;
        }

        else if(count2 == 0){

            candidate2 = num;
            count2 = 1;
        }

        else{

            count1--;
            count2--;
        }
    }

    count1 = 0;
    count2 = 0;

    for(int num : nums){

        if(num == candidate1) count1++;

        else if(num == candidate2) count2++;
    }

    List<Integer> ans =
        new ArrayList<>();

    int limit = nums.length / 3;

    if(count1 > limit)
        ans.add(candidate1);

    if(count2 > limit)
        ans.add(candidate2);

    return ans;
}
```

---

# 22. Kadane's Algorithm Pattern

## Problems

* Maximum Subarray Sum
* Print Maximum Sum Subarray
* Maximum Product Subarray

---

# A) Kadane's Algorithm

## Core Idea

If current sum becomes negative:

```text
Discard it
```

because it can only reduce future answers.

---

## Interview Explanation

### State

```text
currentSum
maxSum
```

### Observation

Negative prefix hurts future sums.

Start a new subarray.

---

## Recognition Clues

```text
Maximum Subarray Sum
Largest Contiguous Sum
```

Think:

```text
Kadane
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int maxSubArray(int[] nums) {

    int sum = 0;

    int maxSum =
        Integer.MIN_VALUE;

    for(int num : nums){

        sum += num;

        maxSum =
            Math.max(maxSum, sum);

        if(sum < 0){

            sum = 0;
        }
    }

    return maxSum;
}
```

---

# B) Print Maximum Sum Subarray

## Core Idea

Track start and end indices.

---

## Interview Explanation

### State

```text
start
end
tempStart
```

### Observation

Whenever a better answer is found:

```text
Store boundaries
```

---

## Recognition Clues

```text
Print Maximum Subarray
Return Indices
```

Think:

```text
Kadane + Indices
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int[] maxSubArrayIndices(
    int[] nums
){

    int sum = 0;

    int maxSum =
        Integer.MIN_VALUE;

    int start = 0;
    int end = 0;

    int tempStart = 0;

    for(int i = 0; i < nums.length; i++){

        if(sum == 0){

            tempStart = i;
        }

        sum += nums[i];

        if(sum > maxSum){

            maxSum = sum;

            start = tempStart;
            end = i;
        }

        if(sum < 0){

            sum = 0;
        }
    }

    return new int[]{
        start,
        end
    };
}
```

---

# C) Maximum Product Subarray

## Core Idea

Negative numbers can flip:

```text
Maximum ↔ Minimum
```

Hence maintain both.

---

## Interview Explanation

### State

```text
prefixProduct
suffixProduct
```

or

```text
currentMax
currentMin
```

### Observation

Negative × Negative

```text
Positive
```

Therefore minimum product can become maximum later.

---

## Recognition Clues

```text
Maximum Product
Subarray Product
Negative Numbers
```

Think:

```text
Track Max and Min
```

---

## TC / SC

| Time | Space |
| ---- | ----- |
| O(N) | O(1)  |

---

## Java Code

```java
public int maxProduct(int[] nums) {

    int currentMax = nums[0];
    int currentMin = nums[0];

    int answer = nums[0];

    for(int i = 1; i < nums.length; i++){

        int num = nums[i];

        if(num < 0){

            int temp =
                currentMax;

            currentMax =
                currentMin;

            currentMin =
                temp;
        }

        currentMax =
            Math.max(
                num,
                currentMax * num
            );

        currentMin =
            Math.min(
                num,
                currentMin * num
            );

        answer =
            Math.max(
                answer,
                currentMax
            );
    }

    return answer;
}
```

---

# Quick Revision Table

| Problem                  | Pattern                  |
| ------------------------ | ------------------------ |
| Two Sum                  | Complement Lookup        |
| Sort 0 1 2               | Dutch National Flag      |
| Majority Element-I       | Boyer Moore              |
| Majority Element-II      | Extended Boyer Moore     |
| Maximum Subarray Sum     | Kadane                   |
| Print Maximum Subarray   | Kadane + Indices         |
| Maximum Product Subarray | Max/Min Product Tracking |

---

# Interview Shortcut

| Question Clue              | Pattern              |
| -------------------------- | -------------------- |
| Pair Sum Target            | Complement           |
| 0 1 2 Sorting              | DNF                  |
| More than N/2              | Boyer Moore          |
| More than N/3              | Extended Boyer Moore |
| Maximum Sum Subarray       | Kadane               |
| Print Maximum Sum Subarray | Kadane + Boundaries  |
| Maximum Product            | Max + Min Tracking   |

---

# 23. Alternate Placement Pattern

## Problems

- Rearrange Array Elements by Sign

## Core Idea

Place positive and negative numbers in alternate positions while maintaining relative order.

## Interview Explanation

### State

```text
positiveIndex = 0
negativeIndex = 1
```

### Task

Place positives at even indices and negatives at odd indices.

### Observation

```text
Equal number of positives and negatives.

Positive -> even index
Negative -> odd index
```

## Recognition Clues

```text
Alternate positive negative
Rearrange by sign
Maintain relative order
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N) | O(N) |

## Java Code

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];

        int pos = 0;
        int neg = 1;

        for(int num : nums){
            if(num > 0){
                ans[pos] = num;
                pos += 2;
            }
            else{
                ans[neg] = num;
                neg += 2;
            }
        }

        return ans;
    }
}
```

## Quick Revision

```text
Positive -> even index
Negative -> odd index

Two placement pointers
```

---

# 24. Permutation Pattern

## Problems

- Next Permutation

## Core Idea

Find the next lexicographically greater arrangement.

## Interview Explanation

### State

```text
breakPoint
successor
```

### Task

Generate next permutation in-place.

### Observation

From right side:

1. Find first decreasing element.
2. Find next larger element.
3. Swap.
4. Reverse suffix.

## Recognition Clues

```text
Next greater arrangement
Lexicographical order
Next permutation
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N) | O(1) |

## Java Code

```java
class Solution {
    public void nextPermutation(int[] nums) {

        int index = -1;
        int n = nums.length;

        for(int i = n - 2; i >= 0; i--){
            if(nums[i] < nums[i + 1]){
                index = i;
                break;
            }
        }

        if(index == -1){
            reverse(nums, 0, n - 1);
            return;
        }

        for(int i = n - 1; i > index; i--){
            if(nums[i] > nums[index]){
                swap(nums, i, index);
                break;
            }
        }

        reverse(nums, index + 1, n - 1);
    }

    private void reverse(int[] arr, int l, int r){
        while(l < r){
            swap(arr, l++, r--);
        }
    }

    private void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

## Quick Revision

```text
Find breakpoint

nums[i] < nums[i+1]

Swap with next greater

Reverse suffix
```

---

# 25. HashSet Sequence Pattern

## Problems

- Longest Consecutive Sequence

## Core Idea

Start counting only from sequence beginnings.

## Interview Explanation

### State

```text
HashSet
currentNum
count
```

### Task

Find longest consecutive sequence.

### Observation

If:

num - 1 exists

then current number is not sequence start.

Only start when:

num - 1 does not exist

## Recognition Clues

```text
Consecutive numbers
Sequence length
Longest streak
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N) | O(N) |

## Java Code

```java
class Solution {
    public int longestConsecutive(int[] nums) {

        HashSet<Integer> set = new HashSet<>();

        for(int num : nums){
            set.add(num);
        }

        int longest = 0;

        for(int num : nums){

            if(!set.contains(num - 1)){

                int current = num;
                int count = 1;

                while(set.contains(current + 1)){
                    current++;
                    count++;
                }

                longest = Math.max(longest, count);
            }
        }

        return longest;
    }
}
```

## Quick Revision

```text
Sequence starts only when

num - 1 absent

Expand right
Count length
```

---

# 26. Matrix Marking Pattern

## Problems

- Set Matrix Zeroes

## Core Idea

Use first row and first column as marker arrays.

## Interview Explanation

### State

```text
matrix[0][j]
matrix[i][0]

col0
```

### Task

If a cell is zero, make entire row and column zero.

### Observation

Extra O(M+N) space can be avoided.

Use first row and first column as markers.

## Recognition Clues

```text
Row marking
Column marking
Matrix update
Zero entire row/column
```

## TC / SC

| Time | Space |
|--------|--------|
| O(M*N) | O(1) |

## Java Code

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int m = matrix.length;
        int n = matrix[0].length;

        int col0 = 1;

        for(int i = 0; i < m; i++){

            if(matrix[i][0] == 0){
                col0 = 0;
            }

            for(int j = 1; j < n; j++){

                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for(int i = m - 1; i >= 0; i--){

            for(int j = n - 1; j >= 1; j--){

                if(matrix[i][0] == 0 ||
                   matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }

            if(col0 == 0){
                matrix[i][0] = 0;
            }
        }
    }
}
```

## Quick Revision

```text
First row -> column markers

First column -> row markers

Need col0 separately
```

---

# 27. Matrix Transformation Pattern

## Problems

- Rotate Matrix By 90 Degrees

## Core Idea

Transpose + Reverse Rows

## Interview Explanation

### State

```text
transpose
reverse
```

### Task

Rotate matrix 90° clockwise.

### Observation

```text
Transpose

then

Reverse every row
```

## Recognition Clues

```text
Rotate matrix
90 degree clockwise
In-place matrix rotation
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N²) | O(1) |

## Java Code

```java
class Solution {
    public void rotate(int[][] matrix) {

        int n = matrix.length;

        for(int i = 0; i < n; i++){

            for(int j = i + 1; j < n; j++){

                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for(int[] row : matrix){

            int left = 0;
            int right = n - 1;

            while(left < right){

                int temp = row[left];
                row[left] = row[right];
                row[right] = temp;

                left++;
                right--;
            }
        }
    }
}
```

## Quick Revision

```text
Transpose

Reverse rows

Done
```

---

# 28. Matrix Boundary Traversal Pattern

## Problems

- Spiral Matrix

## Core Idea

Shrink boundaries after traversal.

## Interview Explanation

### State

```text
top
bottom
left
right
```

### Task

Traverse matrix in spiral order.

### Observation

After completing one boundary:

```text
top++
right--
bottom--
left++
```

## Recognition Clues

```text
Spiral traversal
Boundary traversal
Clockwise matrix walk
```

## TC / SC

| Time | Space |
|--------|--------|
| O(M*N) | O(1) |

## Java Code

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        List<Integer> ans = new ArrayList<>();

        int top = 0;
        int bottom = matrix.length - 1;
        int left = 0;
        int right = matrix[0].length - 1;

        while(top <= bottom &&
              left <= right){

            for(int i = left; i <= right; i++)
                ans.add(matrix[top][i]);

            top++;

            for(int i = top; i <= bottom; i++)
                ans.add(matrix[i][right]);

            right--;

            if(top <= bottom){
                for(int i = right; i >= left; i--)
                    ans.add(matrix[bottom][i]);

                bottom--;
            }

            if(left <= right){
                for(int i = bottom; i >= top; i--)
                    ans.add(matrix[i][left]);

                left++;
            }
        }

        return ans;
    }
}
```

## Quick Revision

```text
top
bottom
left
right

Shrink boundaries
```

---

# 29. Pascal Triangle / Combinatorics Pattern

## Problems

- Pascal's Triangle

## Core Idea

Every value is built from previous row.

## Interview Explanation

### State

```text
nCr
row
column
```

### Task

Generate Pascal Triangle.

### Observation

```text
Current Value

=
Upper Left
+
Upper Right
```

Or:

```text
nCr
```

## Recognition Clues

```text
Pascal Triangle
nCr
Combinations
Binomial coefficient
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N²) | O(1) extra |

## Java Code

```java
class Solution {

    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> ans =
                new ArrayList<>();

        for(int row = 0; row < numRows; row++){

            List<Integer> temp =
                    new ArrayList<>();

            long value = 1;

            for(int col = 0; col <= row; col++){

                temp.add((int)value);

                value =
                    value * (row - col)
                    / (col + 1);
            }

            ans.add(temp);
        }

        return ans;
    }
}
```

## Quick Revision

```text
nCr generation

value =
value*(row-col)/(col+1)
```

---

# 30. Sorting + Two Pointer Pattern

## Problems

- 3 Sum
- 4 Sum

## Core Idea

Sort first, then reduce to Two Sum.

## Interview Explanation

### State

```text
i
left
right
```

### Task

Find triplets/quads satisfying target.

### Observation

After sorting:

```text
Fix one/two elements

Use two pointers
```

Duplicates must be skipped.

## Recognition Clues

```text
Triplets
Quadruplets
Target sum
Unique combinations
```

## TC / SC

| Problem | Time | Space |
|----------|--------|--------|
| 3 Sum | O(N²) | O(1) |
| 4 Sum | O(N³) | O(1) |

## 3 Sum Java Code

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {

        Arrays.sort(nums);

        List<List<Integer>> ans =
                new ArrayList<>();

        int n = nums.length;

        for(int i = 0; i < n; i++){

            if(i > 0 &&
               nums[i] == nums[i - 1])
                continue;

            int left = i + 1;
            int right = n - 1;

            while(left < right){

                int sum =
                    nums[i] +
                    nums[left] +
                    nums[right];

                if(sum < 0){
                    left++;
                }
                else if(sum > 0){
                    right--;
                }
                else{

                    ans.add(Arrays.asList(
                        nums[i],
                        nums[left],
                        nums[right]
                    ));

                    left++;
                    right--;

                    while(left < right &&
                          nums[left] ==
                          nums[left - 1])
                        left++;

                    while(left < right &&
                          nums[right] ==
                          nums[right + 1])
                        right--;
                }
            }
        }

        return ans;
    }
}
```

## Quick Revision

```text
Sort

Fix i

Two Sum using
left/right

Skip duplicates
```

---

# 31. Interval Merging Pattern

## Problems

- Merge Overlapping Intervals

## Core Idea

Sort by start time and merge overlaps.

## Interview Explanation

### State

```text
currentStart
currentEnd
```

### Task

Merge all overlapping intervals.

### Observation

If:

currentStart <= previousEnd

Then overlap exists.

Merge:

```text
end =
max(previousEnd,
currentEnd)
```

## Recognition Clues

```text
Intervals
Ranges
Meeting schedules
Overlapping segments
```

## TC / SC

| Time | Space |
|--------|--------|
| O(N log N) | O(N) |

## Java Code

```java
class Solution {
    public int[][] merge(int[][] intervals) {

        Arrays.sort(
            intervals,
            (a,b) ->
                Integer.compare(a[0], b[0])
        );

        List<int[]> merged =
                new ArrayList<>();

        for(int[] interval : intervals){

            if(merged.isEmpty() ||
               merged.get(
                    merged.size()-1
               )[1] < interval[0]){

                merged.add(interval);
            }
            else{

                merged.get(
                    merged.size()-1
                )[1] = Math.max(
                        merged.get(
                            merged.size()-1
                        )[1],
                        interval[1]
                );
            }
        }

        return merged.toArray(
                new int[merged.size()][]
        );
    }
}
```

## Quick Revision

```text
Sort by start

Overlap?

currentStart <= previousEnd

Merge

end = max(end1,end2)
```
---
