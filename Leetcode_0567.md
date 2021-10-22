Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

sliding window經典題，套路，背起來就對了。

```cpp
class Solution {
public:
    bool checkInclusion(string s1, string s2) 
    {
        unordered_map<char,int> need,window;
        int left = 0,right = 0,len = s2.size();
        int valid = 0;
        for(auto c:s1) need[c]++;
        
        while(right<len)
        {
            char c = s2[right];
            right++;
            
            if(need.count(c))
            {
                window[c]++;
                if(need[c] == window[c])
                {
                    valid++;
                }
            }            
            while(right-left>=s1.size())
            {
                if(valid == need.size())
                    return true;
                char d = s2[left];
                left++;                
                if(need.count(d))
                {
                    if(need[d] == window[d])
                        valid--;
                    window[d]--;
                }
            }
        }        
        return false;
    }
};
```

Runtime: 21 ms, faster than 29.62% of C++ online submissions for Permutation in String.

Memory Usage: 7.5 MB, less than 26.75% of C++ online submissions for Permutation in String.
