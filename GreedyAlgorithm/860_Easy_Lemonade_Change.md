## 860 Lemonade Change - Easy

### Description

At a lemonade stand, each lemonade costs `$5`. 

Customers are standing in a queue to buy from you, and order one at a time (in the order specified by `bills`).

Each customer will only buy one lemonade and pay with either a `$5`, `$10`, or `$20` bill. You must provide the correct change to each customer, so that the net transaction is that the customer pays $5.

Note that you don't have any change in hand at first.

Return `true` if and only if you can provide every customer with correct change.



### Examples

```pseudocode
Example 1:
Input: [5,5,5,10,20]
Output: true
Explanation: 
From the first 3 customers, we collect three $5 bills in order.
From the fourth customer, we collect a $10 bill and give back a $5.
From the fifth customer, we give a $10 bill and a $5 bill.
Since all customers got correct change, we output true.

Example 2:
Input: [5,5,10]
Output: true

Example 3:
Input: [10,10]
Output: false

Example 4:
Input: [5,5,10,10,20]
Output: false
Explanation: 
From the first two customers in order, we collect two $5 bills.
For the next two customers in order, we collect a $10 bill and give back a $5 bill.
For the last customer, we can't give change of $15 back because we only have two $10 bills.
Since not every customer received correct change, the answer is false.
```



### Constraints

- $0 <= bills.length <= 10000$
- `bills[i]` will be either `5`, `10`, or `20`.



### Solution

```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        # define two counters to store the number of $5 and $10 changes we have
        five = ten = 0
        
        # loop over the bills to deal with each customer's bill
        for bill in bills:
            if bill == 5:
                five += 1
            # if the customer's bill is $10, we have to give them $5 as a change
            elif bill == 10:
                if not five:
                    return False
                five -= 1
                ten += 1
            # if the customer's bill is $20, we have to give them $15 in total back
            else:
                # one $5 and one $10
                if five and ten:
                    five -= 1
                    ten -= 1
                # three $5
                elif five >= 3:
                    five -= 3
                else:
                    return False
            
        return True
```



#### Complexity Analysis

- Time Complexity: $O(N)$, where $N$ is the length of `bills`
- Space Complexity: $O(1)$ 