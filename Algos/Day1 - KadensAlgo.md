# 🚀 Kadane's Algorithm - Problem Solutions

## 📅 Day 1

### 📊 Summary

- **Total Problems Solved**: 5  
  - **Easy**: 2
  - **Medium**: 3

---

### 1. [Maximum Subarray (Medium)](https://leetcode.com/problems/maximum-subarray/)

#### 📝 Problem Description

Find the contiguous subarray with the largest sum.

> **Note:** Though labeled "Medium," this problem is a direct application of Kadane's Algorithm and could be considered **"Easy."**

---

#### 💡 Approach

> 🧠 **Tip:** Think of walking through the array and keeping a running total.  
> If your current sum drops below zero, it’s better to **start fresh** from the next number.  
> Kadane’s Algorithm does exactly this — it keeps track of the current subarray sum (`curr_max`) and resets it if continuing the current subarray is no longer beneficial.
---

##### 🔧 Variables Used:

- `global_max`: Tracks the maximum subarray sum found.
- `curr_max`: Tracks the sum of the current subarray.

##### 📌 Algorithm Steps:

1. Initialize both `global_max` and `curr_max` with `nums[0]`.
2. Iterate through the array (from index 1 to end):
   - Update `curr_max`:
     ```python
     curr_max = max(nums[i], curr_max + nums[i])
     ```
     (Start a new subarray if `nums[i]` is greater.)
   - Update `global_max`:
     ```python
     global_max = max(global_max, curr_max)
     ```
3. Return `global_max`.

---

#### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(n)`  
- **Space Complexity**: `O(1)`

---


### 2. [Maximum Sum Circular Subarray (Medium)](https://leetcode.com/problems/maximum-sum-circular-subarray/)

#### 📝 Problem Description

Find the contiguous subarray (possibly wrapping around the end) with the largest sum.

---

#### 💡 Approach

> 🥧 **Tip:** Imagine the array as a circular pie. You want the maximum slice — which can either be:
> 1. The regular (non-circular) subarray — handled with Kadane’s Algorithm.
> 2. The circular one — which is the total sum minus the smallest subarray (the part you "cut out").

---

##### 🔧 Variables Used:

- `global_max`: Tracks the maximum subarray sum found.
- `curr_max`: Tracks the sum of the current subarray for max.
- `global_min`: Tracks the minimum subarray sum found.
- `curr_min`: Tracks the sum of the current subarray for min.
- `total`: Total sum of all elements in the array.

---

##### 📌 Algorithm Steps:

1. Initialize `global_max`, `curr_max`, `global_min`, `curr_min`, and `total` with `nums[0]`.
2. Iterate through the array starting from index 1:
    - Update `curr_max`:
      ```python
      curr_max = max(nums[i], curr_max + nums[i])
      ```
      (Start new subarray if `nums[i]` alone is better.)
    - Update `global_max`:
      ```python
      global_max = max(global_max, curr_max)
      ```
    - Update `curr_min`:
      ```python
      curr_min = min(nums[i], curr_min + nums[i])
      ```
    - Update `global_min`:
      ```python
      global_min = min(global_min, curr_min)
      ```
    - Accumulate `total`:
      ```python
      total += nums[i]
      ```

3. Final result:
    - If all numbers are negative, return `global_max` (max of negative values).
    - Else, return:
      ```python
      max(global_max, total - global_min)
      ```

---

#### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(n)`  
- **Space Complexity**: `O(1)`

### 3. [Maximum Value of a String in an Array (Easy)](https://leetcode.com/problems/maximum-value-of-a-string-in-an-array/)

#### 📝 Problem Description

You're given an array of strings.  
If a string consists only of digits, treat it as a number.  
Otherwise, treat its value as the length of the string.  

Return the **maximum value** among all strings after applying this rule.

---

#### 💡 Approach

> 🧠 **Tip:** Modify the original array in-place by converting each string into either an integer or its length to avoid using extra space.

---

##### 🔧 Variables Used:

- `result`: Tracks the maximum value encountered (either numeric or string length).

---

##### 📌 Algorithm Steps:

1. Initialize `result` to `0`.
2. Iterate through the list:
    - For each element, check if it’s numeric:
      ```python
      if nums[i].isnumeric():
          nums[i] = int(nums[i])
      else:
          nums[i] = len(nums[i])
      ```
      (This converts the element to its value so we can directly use it in the next step.)
    - Update `result`:
      ```python
      result = max(result, nums[i])
      ```

3. Return `result`.

---

#### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(n)`  
- **Space Complexity**: `O(1)` (in-place modification)

### 4. [Maximum Product Subarray (Medium)](https://leetcode.com/problems/maximum-product-subarray)

#### 📝 Problem Description

Find the contiguous subarray within a given array (containing at least one number) that has the largest product.  
Return the product of that subarray.

---

#### 💡 Approach

> ⚠️ **Tip:** The product can become negative, and multiplying two negative numbers can turn it positive — so we track both `max` and `min` products at every step.

---

##### 🔧 Variables Used:

- `global_max`: Keeps track of the overall maximum product found.
- `curr_max`: Tracks the current maximum product ending at the current index.
- `curr_min`: Tracks the current minimum product ending at the current index (used for handling negatives).
- `temp_curr_max`: Temporarily holds the new `curr_max` before updating it.

---

##### 📌 Algorithm Steps:

1. Initialize `global_max`, `curr_max`, and `curr_min` with `nums[0]`.
2. Iterate through the array starting from index 1:
    - Calculate temporary maximum product:
      ```python
      temp_curr_max = max(nums[i], curr_max * nums[i], curr_min * nums[i])
      ```
    - Update current minimum product:
      ```python
      curr_min = min(nums[i], curr_max * nums[i], curr_min * nums[i])
      ```
    - Update current maximum product:
      ```python
      curr_max = temp_curr_max
      ```
    - Update global maximum:
      ```python
      global_max = max(global_max, curr_max)
      ```
3. Return `global_max`.

---

#### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(n)`  
- **Space Complexity**: `O(1)`


### 5. [Degree of an Array (Easy)](https://leetcode.com/problems/degree-of-an-array/)

#### 📝 Problem Description

Find the smallest possible length of a contiguous subarray that has the same **degree** as the entire array.

> The **degree** of an array is defined as the maximum frequency of any one of its elements.

---

#### 💡 Approach

> 🧠 **Tip:** The shortest subarray with the same degree must span from the **first** to the **last** occurrence of the element(s) that appear most frequently.

---

##### 🔧 Variables Used:

- `min_length`: Tracks the minimum subarray length that matches the degree.
- `count`: A dictionary to count occurrences of each element.
- `degree`: The maximum frequency (i.e., the degree) in the array.

---

##### 📌 Algorithm Steps:

1. Use a dictionary (`count`) to store the frequency of each number.
2. Calculate the `degree` using the maximum value from `count.values()`.
3. Initialize `min_length` with `len(nums)` (as the worst case).
4. For each number `n` with frequency `c` in `count.items()`:
    - If `c` equals the degree:
      - Find the **first** and **last** occurrence of `n` in `nums`.
      - Calculate the subarray length and update `min_length`:
        ```python
        start = nums.index(n)
        end = len(nums) - nums[::-1].index(n) - 1
        min_length = min(min_length, end - start + 1)
        ```
5. Return `min_length`.

---

#### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(n)`  
- **Space Complexity**: `O(n)`

