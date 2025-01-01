---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - Strings
  - Design-Pattern
---

# 🚀 _Day 1. Implement Atoi_ 🧠

The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/string-gfg-160/problem/implement-atoi)

## 💡 **Problem Description:**

You are given a string `s` that represents a potential integer value. Your task is to implement the **atoi()** function, which converts the string to an integer, following these steps:

1. Skip any leading whitespaces.
2. Check for a sign (`+` or `-`), default to positive if no sign is present.
3. Read the integer by ignoring leading zeros until a non-digit character is encountered or end of the string is reached. If no digits are present, return 0.
4. Handle overflow: If the result exceeds the 32-bit signed integer range (`[-2^31, 2^31 - 1]`), return the appropriate bound.
   
## 🔍 **Example Walkthrough:**

**Input:**  
`s = "-123"`  
**Output:**  
`-123`  

**Explanation:**  
The string can be converted to the integer `-123`, which is within the 32-bit signed integer range.

**Input:**  
`s = "  -"`  
**Output:**  
`0`  

**Explanation:**  
No digits are present after the sign, so the result is 0.

**Input:**  
`s = " 1231231231311133"`  
**Output:**  
`2147483647`  

**Explanation:**  
The string exceeds the maximum 32-bit signed integer, so the result is clamped to `2147483647`.

**Input:**  
`s = "-999999999999"`  
**Output:**  
`-2147483648`  

**Explanation:**  
The string is below the minimum 32-bit signed integer, so the result is clamped to `-2147483648`.

**Input:**  
`s = "  -0012gfg4"`  
**Output:**  
`-12`  

**Explanation:**  
The string converts to `-12`, ignoring the non-digit character `g`.

### Constraints:
- `1 ≤ |s| ≤ 15`
- The string length will be between 1 and 15 characters.

## 🎯 **My Approach:**

1. **Skip Leading Whitespaces**:  
   We begin by skipping any leading whitespace characters to focus on the number.

2. **Handle Signs**:  
   If the next character is a sign (`+` or `-`), we determine whether the result should be positive or negative.

3. **Read Digits**:  
   As we read digits, we accumulate the result. If a non-digit character is encountered, we stop processing.

4. **Handle Overflow**:  
   If the result exceeds the limits of a 32-bit signed integer (`-2^31` to `2^31 - 1`), return the appropriate boundary value.

5. **Return the Result**:  
   The final integer is returned after handling potential overflow and sign.

## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O(n), where `n` is the length of the string. We iterate through the string only twice: once to skip spaces and check the sign, and once to process the digits.
- **Expected Auxiliary Space Complexity:** O(1), as we only use a constant amount of additional space to store variables for the result and current index.

## 📝 **Solution Code**


## Code (Cpp)

```cpp
class Solution {
public:
    int myAtoi(char *s) {
        int idx = 0, sign = 1;
        long res = 0;

        while (s[idx] == ' ') idx++;

        if (s[idx] == '-' || s[idx] == '+') {
            sign = (s[idx++] == '-') ? -1 : 1;
        }

        while (s[idx] >= '0' && s[idx] <= '9') {
            res = res * 10 + (s[idx++] - '0');

            if (res * sign > INT_MAX) return INT_MAX;
            if (res * sign < INT_MIN) return INT_MIN;
        }

        return static_cast<int>(res * sign);
    }
};
```