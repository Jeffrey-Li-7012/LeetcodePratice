## 455 Assign Cookies -Easy 

[Link to the original question](https://leetcode.com/problems/assign-cookies/)

### Description

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie. Each child $i$ has a greed factor $g_i$, which is the minimum size of a cookie that the child will be content with; and each cookie $j$ has a size $s_j$. If $s_j$ >= $g_i$, we can assign the cookie j to the child $i$, and the child $i$ will be content. Your goal is to maximize the number of your content children and output the maximum number.



### Notes

- You may assume the greed factor is always positive.
- You cannot assign more than one cookie to one child.



### Examples

```pseudocode
Example 1:
Input: [1,2,3], [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.

Example 2:
Input: [1,2], [1,2,3]

Output: 2

Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
```



### Algorithm（Strategy）

贪心算法+双指针求解

给一个孩子的饼干应当尽量小并且能满足孩子，大的留来满足胃口大的孩子。因为胃口小的孩子最容易得到满足，所以优先满足胃口小的孩子需求。按照从小到大的顺序使用饼干尝试是否可满足某个孩子。



### Key Points

将greed factor g 和 cookie size s 分别从小到大进行排序，使用贪心思想，配合双指针，每个饼干只尝试一次，成功则换下一个孩子来尝试。



### Solution

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        
        child = 0 # 指向greed factor列表的指针，也作为已经满足的chlid的计数器（结果）
        cookie = 0 # 指向cookie size列表的指针
        while child < len(g) and cookie < len(s):
            # 如果当前的child可以被当前的cookie所满足，则child指针移动至下一位
            if g[child] <= s[cookie]:
                child += 1
            # 无论当前child是否满足，cookie指针都要移向下一位
            cookie += 1
                
        
        return child
```



#### Complexity Analysis

- Time Complexity: $O(Nlog(N))$, where $N$ is the maximum of length of list g and list s. Because we sort those two lists.

- Space Complexity: $O(1)$

  