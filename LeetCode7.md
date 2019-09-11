# 7. Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

    Input: 123
    Output: 321
    
**Example 2:**

    Input: -123
    Output: -321

**Example 3:**

    Input: 120
    Output: 21

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: 
[−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

#### 題意：

給一整數，返回逆序的數字。若超過integer範圍則返回0

#### 思路：

難點在要注意組合逆序數字時會有overflow的狀況(暫存值*10)
把判斷放在最後return，然後暫存值用64-bit的變數宣告


#### 參考code：

```cpp
class Solution 
{
public:
    int reverse(int x) 
    {
        long long nReverse = 0;
        while(x)
        {
            nReverse = nReverse*10 + x%10;
            x /= 10;
        }
        return (nReverse > INT_MAX || nReverse <INT_MIN)? 0 : nReverse;
    }
};
```

Runtime: 4 ms, faster than 68.32%

Memory Usage: 8.1 MB, less than 100.00%

