# 131. Palindrome Partitioning

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

**Example:**

    Input: "aab"
    Output:
    [
      ["aa","b"],
      ["a","a","b"]
    ]
    
#### 題目大意：
找出"所有"子字串為回文的組合

一開始想法是對的，但寫太久就找答案了......

DP和回溯法都可以解，注意以後關鍵字有找出"所有"的話，就優先考慮回溯法

#### 參考code：
```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) 
    {
        vector<vector<string>> vvAns;
        BackTrace(vvAns,{},s);
        return vvAns;
    }
private:
    bool isPalindrome(string strText)
    {
        if(strText.size()<=1)
            return true;
        int start = 0,tail = strText.size()-1;
        while(start <= tail)
        {
            if(strText[start++] != strText[tail--])
                return false;
        }
        return true;
    }
    
    void BackTrace(vector<vector<string>>& vvAns,vector<string> vAns,string strText)
    {
        if(strText.empty())
        {
            vvAns.push_back(vAns);
            return;
        }
        for(int i = 1; i<=strText.size();++i)
        {
            string strTemp = strText.substr(0,i);
            if(isPalindrome(strTemp))
            {
                vAns.push_back(strTemp);
                BackTrace(vvAns,vAns,strText.substr(i));
                vAns.pop_back();
            }
        }        
    }
};
```

Runtime: 64 ms, faster than 22.83%

Memory Usage: 60.8 MB, less than 25.00%
