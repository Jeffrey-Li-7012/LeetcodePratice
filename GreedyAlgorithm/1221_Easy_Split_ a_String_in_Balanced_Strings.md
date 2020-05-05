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

1. 创建两个计数器，`result` 和 `balance_variable` ，其中`result` 用来记录遇到的balanced string的个数，而`balance_variable` 用来记录在扫描过程中，遇到“L”比遇到“R”多多少个。
2. 从左到右扫描输入的String，如果遇到“L”则`balance_variable`加,1，遇到“R”就减1。
3. 一旦`balance_variable`变为0，表明已经扫描到一个balanced string了，记录`result`就加1。



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

#### Complexity Analysis:

- Time Complexity: $O(n)$ , where $n$ is the length of the input string. Because you scan through the whole input string.
- Space Complexity:  $O(n)$, where n is the length of the input string. Because you just need to store the string.