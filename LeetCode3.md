# 3. Longest Substring Without Repeating Characters

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

    Input: "abcabcbb"
    Output: 3 
    Explanation: The answer is "abc", with the length of 3. 

**Example 2:**

    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.

**Example 3:**

    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
    Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

#### 題意：

找出最長不重複的"子"字串。

#### 思路：

初見殺。沒看過應該是寫不出來...

但基本上以map思考解法是正確的，不過眉眉角角兜一兜，一堆小問題大概就fail了。

先假設最長子字串，由index left開始，到index right結束。
從字串第一個字開始進map，若沒在map內則將字元寫入map，並把index right附值給map[字元]
若在map內，則將index left偏移，由原left和mp[s[right]]+1比較誰大則代替left
最後更新Ans值 判斷原值和right-left+1哪個大 取代Ans值

#### 參考code：

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) 
    {
        unordered_map<char,int> mp;
        int left = 0,nAns = 0;
        for(int right = 0; right <s.size();++right)
        {
            if(mp.count(s[right]))
            {
                left = max(left,mp[s[right]]+1);
            }
            mp[s[right]] = right;
            nAns = max(nAns,right-left+1);
        }
        return nAns;
    }
};
```

Runtime: 24 ms, faster than 47.39%

Memory Usage: 10.9 MB, less than 53.73% 

