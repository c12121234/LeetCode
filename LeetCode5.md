# 5. Longest Palindromic Substring

**Example 1:**

    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.

**Example 2:**

    Input: "cbbd"
    Output: "bb"
    
#### 題意：

找出最長的回文字串

#### 思路：

有回文的題目可以考慮使用DP來解，只是效率不保證就是了。
核心想法是，若dp[i][j]要為回文的話，則dp[i+1][j-1]一定為回文 (i,j分別為起始和終點的index值)

#### 參考code：

```cpp
class Solution {
public:
    string longestPalindrome(string s) 
    {
        int N = s.size();
        if(N == 0)
            return "";
        string strAns = s.substr(0,1);
        vector<vector<int>> dp(N,vector<int>(N,0));
        for(int i = 0; i<N;++i)
        {
            for(int j = 0; j<i;++j)
            {
                dp[j][i] = (s[i] == s[j]) && (i == j+1 || dp[j+1][i-1]);
                if(dp[j][i] && i-j+1 >= strAns.size())
                    strAns = s.substr(j,i-j+1);
            }
            dp[i][i] = 1;
        }
        return strAns;
    }
};
```

Runtime: 252 ms, faster than 14.49%

Memory Usage: 194.6 MB, less than 5.51%

我去，這啥效能...
