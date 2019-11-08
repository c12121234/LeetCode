# 22. Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

    [
      "((()))",
      "(()())",
      "(())()",
      "()(())",
      "()()()"
    ]

#### 思路

找全部組合大多從back trace下手

注意")"的數量增加條件為"("數量大於")"時

避免造成開口向外的圖形發生

#### 參考code

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) 
    {
        vector<string> vAns;
        string strText("");
        DFS(vAns,strText,n,0,0);
        return vAns;
    }
private:
    void DFS(vector<string>& vs,string strText,int n, int left, int right)
    {
        if(n == left && n == right)
        {
            vs.push_back(strText);
            return;
        }
        if(left < n)
        {
            DFS(vs,strText+"(",n,left+1,right);
        }
        if(right < left)
        {
            DFS(vs,strText+")",n,left,right+1);
        }
        
        
    }
};
```

Runtime: 0 ms

Memory Usage: 17.4 MB

