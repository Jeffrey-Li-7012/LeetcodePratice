## 1221. Split a String in Balanced Strings-EASY

[Link to the original question](https://leetcode.com/problems/split-a-string-in-balanced-strings/)



### Description:

*Balanced* strings are those who have equal quantity of 'L' and 'R' characters.

Given a balanced string `s` split it in the maximum amount of balanced strings.

Return the maximum amount of splitted balanced strings.



### Examples:

```pseudocode
Example 1:
Input: s = "RLRRLLRLRL"
Output: 4
Explanation: s can be split into "RL", "RRLL", "RL", "RL", each substring contains same number of 'L' and 'R'.


Example 2:
Input: s = "RLLLLRRRLR"
Output: 3
Explanation: s can be split into "RL", "LLLRRR", "LR", each substring contains same number of 'L' and 'R'.

Example 3:
Input: s = "LLLLRRRR"
Output: 1
Explanation: s can be split into "LLLLRRRR".

Example 4:
Input: s = "RLRRRLLRLL"
Output: 2
Explanation: s can be split into "RL", "RRRLLRLL", since each substring contains an equal number of 'L' and 'R'
```



### Constraints

- `1 <= s.length <= 1000`
- `s[i] = 'L' or 'R'`



### Algorithm

1. 从左到右扫描输入的String，如果遇到“L”则balanced string的字符计数器加,1，遇到“R”就减1
2. 一旦balanced string的字符计数器的值变为0，表明已经扫描到一个balanced string了，记录结果的计数器就加一



### Solution

```python
class Solution:
    def balancedStringSplit(self, s: str) -> int:
        
        result = 0
        balance_variable = 0
        for char in s:
            if char == "L":
                balance_variable += 1
            else:
                balance_variable -= 1
                
            if balance_variable == 0:
                result += 1
                
        
        return result
```

