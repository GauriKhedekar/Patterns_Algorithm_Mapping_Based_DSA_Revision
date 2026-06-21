# String Pattern Notes for Google Interviews

---

# 1. Remove Outermost Parentheses

**Problem:** LeetCode 1021

---

## Interview Flow

### Clarify

- String contains only valid parentheses?
- Multiple primitive substrings possible?
- Return resulting string after removing outermost brackets?

---

## Brute Force

- Find every primitive substring.
- Remove first and last bracket from each primitive.
- Join all substrings.

### Complexity

- Time: O(N)
- Space: O(N)

---

## Pattern

### Depth Counter Pattern

Whenever:

- '(' increases depth
- ')' decreases depth

Outer parentheses are exactly those where:

- depth = 0 before '('
- depth = 0 after ')'

---

## Plan

- Maintain depth
- Append '(' only if depth > 0
- Append ')' only if depth > 1 before decrement
- Skip outermost brackets

---

## Visualization

```text
Input:

(()())(())

depth

( -> 1 skip
( -> 2 add
) -> 1 add
( -> 2 add
) -> 1 add
) -> 0 skip

Result:
()()
```

---

## Code

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder ans = new StringBuilder();
        int depth = 0;

        for(int i = 0; i < s.length(); i++) {

            if(s.charAt(i) == '(') {

                if(depth > 0) {
                    ans.append('(');
                }

                depth++;
            }
            else {

                depth--;

                if(depth > 0) {
                    ans.append(')');
                }
            }
        }

        return ans.toString();
    }
}
```

---

## Remember

```text
Opening:
Add first?
NO

Closing:
Add last?
NO

Skip depth=0 boundaries
```

---

# 2. Reverse Words In A String

**Problem:** LeetCode 151

---

## Interview Flow

### Clarify

- Multiple spaces possible?
- Leading spaces possible?
- Trailing spaces possible?

---

## Brute Force

- split()
- reverse array
- join

### Complexity

O(N)

But split creates extra arrays.

---

## Pattern

### Reverse Traversal Pattern

Instead of reversing words:

Traverse string from right → left.

---

## Plan

```text
Skip spaces

Find word end

Find word start

Append word

Repeat
```

---

## Visualization

```text
Input

"the sky is blue"

Start from end

blue
is
sky
the

Output

"blue is sky the"
```

---

## Code

```java
class Solution {
    public String reverseWords(String s) {

        StringBuilder ans = new StringBuilder();

        int i = s.length() - 1;

        while(i >= 0) {

            while(i >= 0 && s.charAt(i) == ' ') {
                i--;
            }

            if(i < 0) break;

            int j = i;

            while(j >= 0 && s.charAt(j) != ' ') {
                j--;
            }

            if(ans.length() > 0) {
                ans.append(" ");
            }

            ans.append(s.substring(j + 1, i + 1));

            if(j < 0) break;

            i = j - 1;
        }

        return ans.toString();
    }
}
```

---

## Remember

```text
Right → Left

Skip Spaces

Take Word

Append

Repeat
```

---

# 3. Largest Odd Number In String

**Problem:** LeetCode 1903

---

## Interview Flow

### Clarify

- String contains digits only?
- Need largest odd substring?

---

## Observation

For number to be odd:

```text
Last digit must be odd
```

---

## Pattern

### Suffix Search Pattern

Search from end.

First odd digit found:

Everything before it forms answer.

---

## Visualization

```text
35427

7 odd

Answer

35427
```

```text
35420

2 even
0 even
4 even

5 odd

Answer

35
```

---

## Code

```java
class Solution {
    public String largestOddNumber(String num) {

        int n = num.length();

        for(int i = n - 1; i >= 0; i--) {

            int digit = num.charAt(i) - '0';

            if(digit % 2 == 1) {
                return num.substring(0, i + 1);
            }
        }

        return "";
    }
}
```

---

## Remember

```text
Odd Number

Only last digit matters

Scan from end
```

---

# 4. Longest Common Prefix

**Problem:** LeetCode 14

---

## Interview Flow

### Clarify

- Empty array possible?
- One string possible?

---

## Brute Force

Compare character by character across all strings.

---

## Pattern

### Prefix Shrinking Pattern

Take first string as prefix.

Keep shrinking until every string starts with it.

---

## Plan

```text
prefix = first string

For every string:

while current string
does not start with prefix

shrink prefix

return prefix
```

---

## Visualization

```text
flower
flow
flight

prefix = flower

flow doesn't start with flower

flower
flowe
flow
✔

flight doesn't start with flow

flo
fl
✔

Answer = fl
```

---

## Code

```java
class Solution {

    public String longestCommonPrefix(String[] strs) {

        if(strs == null || strs.length == 0) {
            return "";
        }

        String prefix = strs[0];

        for(int i = 1; i < strs.length; i++) {

            while(!strs[i].startsWith(prefix)) {

                prefix =
                    prefix.substring(0,
                    prefix.length() - 1);
            }

            if(prefix.isEmpty()) {
                return "";
            }
        }

        return prefix;
    }
}
```

---

## Remember

```text
Take First String

Shrink Until Match

Done
```

---

# 5. Isomorphic Strings

**Problem:** LeetCode 205

---

# Method 1 : HashMap

---

## Pattern

### One-To-One Mapping Pattern

```text
a -> x

Valid

a -> x
b -> y
```

```text
a -> x
b -> x

Invalid
```

---

## Code

```java
class Solution {

    public boolean isIsomorphic(String s, String t) {

        HashMap<Character, Character> map =
            new HashMap<>();

        if(s.length() != t.length()) {
            return false;
        }

        for(int i = 0; i < s.length(); i++) {

            char original = s.charAt(i);
            char replacement = t.charAt(i);

            if(!map.containsKey(original)) {

                if(!map.containsValue(replacement)) {
                    map.put(original, replacement);
                }
                else {
                    return false;
                }
            }
            else {

                if(map.get(original) != replacement) {
                    return false;
                }
            }
        }

        return true;
    }
}
```

---

# Method 2 : Array Mapping (Optimal)

---

## Pattern

### Last Seen Position Pattern

Store last occurrence index.

If both characters appeared at same positions before:

Mapping is valid.

---

## Visualization

```text
foo
app

f -> a

o -> p

last seen indexes always match
```

---

## Code

```java
class Solution {

    public boolean isIsomorphic(String s, String t) {

        int[] sMap = new int[256];
        int[] tMap = new int[256];

        if(s.length() != t.length()) {
            return false;
        }

        for(int i = 0; i < s.length(); i++) {

            char sChar = s.charAt(i);
            char tChar = t.charAt(i);

            if(sMap[sChar] != tMap[tChar]) {
                return false;
            }

            sMap[sChar] = i + 1;
            tMap[tChar] = i + 1;
        }

        return true;
    }
}
```

---

## Remember

```text
Same History

Same Mapping

Compare Last Seen Positions
```

---

# 6. Rotate String

**Problem:** LeetCode 796

---

## Interview Flow

### Clarify

- Rotation only?
- Lengths must match?

---

## Pattern

### Double String Pattern

All rotations exist inside:

```text
s + s
```

---

## Visualization

```text
s = abcde

s+s

abcdeabcde
  cdeab

Goal found
```

---

## Code

```java
class Solution {

    public boolean rotateString(String s, String goal) {

        if(s.length() != goal.length()) {
            return false;
        }

        return (s + s).contains(goal);
    }
}
```

---

## Remember

```text
Rotation

↓

s+s

↓

Contains Goal
```

---

# 7. Valid Anagram

**Problem:** LeetCode 242

---

## Interview Flow

### Clarify

- Lowercase only?
- Unicode?

---

## Pattern

### Frequency Count Pattern

Two strings are anagrams if:

```text
Every character count matches
```

---

## Visualization

```text
listen

l=1
i=1
s=1
t=1
e=1
n=1

silent

same frequencies

TRUE
```

---

## Code

```java
class Solution {

    public boolean isAnagram(String s, String t) {

        int[] sMap = new int[256];
        int[] tMap = new int[256];

        if(s.length() != t.length()) {
            return false;
        }

        for(int i = 0; i < s.length(); i++) {

            sMap[s.charAt(i)]++;
            tMap[t.charAt(i)]++;
        }

        for(int i = 0; i < 256; i++) {

            if(sMap[i] != tMap[i]) {
                return false;
            }
        }

        return true;
    }
}
```

---

# GOOGLE INTERVIEW REVISION SHEET

```text
REMOVE OUTER PARENTHESES
→ Depth Counter

REVERSE WORDS
→ Reverse Traversal

LARGEST ODD NUMBER
→ Scan From End

LONGEST COMMON PREFIX
→ Prefix Shrinking

ISOMORPHIC STRINGS
→ Character Mapping

ROTATE STRING
→ (s+s).contains(goal)

VALID ANAGRAM
→ Frequency Count
```

---

# What To Say In Google Interview

For every problem:

1. Clarify constraints

2. Explain brute force

3. Identify pattern

4. Explain plan in 4-5 lines

5. Code while speaking

6. If stuck > 60 sec, talk

7. Dry run one example
