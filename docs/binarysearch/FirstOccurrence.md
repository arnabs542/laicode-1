<!----- Conversion time: 0.509 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* GD2md-html version 1.0β13
* Tue Jan 15 2019 04:33:59 GMT-0800 (PST)
* Source doc: https://docs.google.com/open?id=1vJbgFLU-40mlHwtpMVaRj4svT1shWxSdhF_ejSB1qLc
----->

# First Occurrence

[https://app.laicode.io/app/problem/15](https://app.laicode.io/app/problem/15)

## Description

Given a target integer T and an integer array A sorted in ascending order, find the index of the first occurrence of T in A or return -1 if there is no such index.

Assumptions

- There can be duplicate elements in the array.

Examples

- A = {1, 2, 3}, T = 2, return 1
- A = {1, 2, 3}, T = 4, return -1
- A = {1, 2, 2, 2, 3}, T = 2, return 1

Corner Cases

- What if A is null or A of zero length? We should return -1 in this case.

Medium

Array

Binary Search

## Solution

### Method 1: neighboring method/narrow down the range and check afterward

```java
public class Solution {

  public int firstOccur(int[] array, int target) {
    // Write your solution here
    if (array == null || array.length == 0) {
      return -1;
    }
    int left = 0;
    int right = array.length - 1;
    while (left + 1 < right) {
      int mid = left + (right - left) / 2;
      if (array[mid] < target) {
        left = mid;
      } else {
        right = mid;
      }
    }
    if (array[left] == target) {
      return left;
    } else if (array[right] == target) {
      return right;
    }
    return -1;
  }
}
```

### Method 2: classical binary search

```java
public class Solution {

  public int firstOccur(int[] array, int target) {
    // Write your solution here
    if (array == null || array.length == 0) {
      return -1;
    }
    int start = 0;
    int end = array.length - 1;
    while (start <= end) {
      int mid = start + (end - start) / 2;
      if (array[mid] == target) {
        if (mid > 0 && array[mid - 1] == target) {
          end = mid - 1;
        } else {
          return mid;
        }
      } else if (array[mid] < target) {
        start = mid + 1;
      } else {
        end = mid - 1;
      }
    }
    return -1;
  }
}
```

<!-- GD2md-html version 1.0β13 -->
