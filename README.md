# 🔤 LeetCode 10 - Regular Expression Matching

## 📌 Problem

Given an input string `s` and a pattern `p`, implement regular expression matching with support for:

* `.` → Matches any single character.
* `*` → Matches zero or more of the preceding element.

The matching must cover the **entire input string**.

## 💡 Approach

Use **Dynamic Programming**.

Let `dp[i][j]` represent whether the first `i` characters of `s` match the first `j` characters of `p`.

For each character:

* If the characters match or the pattern contains `.`, move diagonally.
* If the pattern contains `*`, consider:

  * Matching zero occurrences.
  * Matching one or more occurrences.

## 💻 Python Solution

```python id="4r4r6x"
class Solution:
    def isMatch(self, s, p):
        m = len(s)
        n = len(p)

        dp = [[False] * (n + 1) for _ in range(m + 1)]
        dp[0][0] = True

        for j in range(2, n + 1):
            if p[j - 1] == '*':
                dp[0][j] = dp[0][j - 2]

        for i in range(1, m + 1):
            for j in range(1, n + 1):

                if p[j - 1] == '.' or p[j - 1] == s[i - 1]:
                    dp[i][j] = dp[i - 1][j - 1]

                elif p[j - 1] == '*':
                    dp[i][j] = dp[i][j - 2]

                    if p[j - 2] == '.' or p[j - 2] == s[i - 1]:
                        dp[i][j] = dp[i][j] or dp[i - 1][j]

        return dp[m][n]
```

## 🧪 Example

### Input

```text
s = "aa"
p = "a*"
```

### Output

```text
True
```

### Explanation

`a*` means zero or more occurrences of `a`, so it can match `"aa"`.

## ⏱️ Complexity

* **Time Complexity:** `O(m × n)`
* **Space Complexity:** `O(m × n)`

## 🏷️ LeetCode Details

* **Problem:** Regular Expression Matching
* **Problem Number:** 10
* **Difficulty:** Hard
* **Language:** Python

## 🎯 Topics

* Dynamic Programming
* Strings
* Regular Expressions
* Pattern Matching

## 👩‍💻 Author

**Nandhini**
