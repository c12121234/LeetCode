# 1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly*** one solution, and you may not use the same element twice.

**Example:**

    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].
    
#### 題意：

找出兩index值，index對應的值相加為target。假設只有唯一解而且每個元素值只能使用一次。

#### 思路：

超級經典LeetCode第一題。

不知有多少人興致勃勃開始刷leetcode，碰到這題懷疑人生許久的...

老實說解出來不難，但這題要寫的效率高是有點難度的。

O(n<sup>2</sup>)很直觀，效率爛爆

參考code如下：

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
       vector<int> vAns;
        for(int i = 0; i<nums.size();++i)
       {
           for(int j = 0; j<nums.size();++j)
           {
               if(nums[i]+nums[j] == target && i!=j)
               {
                   vAns.push_back(i);
                   vAns.push_back(j);
                   return vAns;
               }
           }
       }
        
        
        return vAns;
    }
};
```

Runtime: 220 ms
Memory Usage: 9.2 MB

這悲慘的執行效率 再看看運用map的解法 O(n)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
       int head = 0,tail = nums.size()-1;
        vector<int> vAns(2,0);
        unordered_map<int,int> mp;
        for(int i = 0; i<nums.size();++i)
            mp[nums[i]] = i;
        for(int i = 0; i<nums.size();++i)
        {
            int nTemp = target-nums[i];
            if(mp.count(nTemp)!=0 && mp[nTemp] != i)
            {
                vAns[0] = i;
                vAns[1] = mp[nTemp];
                break;
            }
        }
        return vAns;
    }
};
```
先將value,index填入map後

再判斷target-nums[i]是否在map中，而且index值不等於自己

Runtime: 12 ms
Memory Usage: 10.5 MB

嘖嘖，效率差了快20倍

最後一個概念也是類似使用map，但先經過排序
且搜尋時使用binary search
找到index值後再轉回原index
也是O(n)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        vector<int> vAns(2,0);
        vector<pair<int,int>> vp;
        for(int i = 0; i<nums.size();++i)
        {
            auto p = make_pair(i,nums[i]);
            vp.push_back(p);
        }
        
        sort(nums.begin(),nums.end());
        int head = 0, tail = nums.size()-1;
        while(head < tail)
        {
            int nTemp = nums[head]+nums[tail];
            if(nTemp > target)
                tail--;
            else if(nTemp < target)
                head++;
            else
                break;
        }
        auto it1 = find_if(vp.begin(),vp.end(),[&nums,head](auto p){return nums[head] == p.second;});
        vAns[0] = it1->first;
        auto it2 = find_if(vp.begin(),vp.end(),[&nums,tail](auto p){return nums[tail] == p.second;});
        if(it1 == it2)
        {
            auto it2 = find_if(it1+1,vp.end(),[&nums,tail](auto p){return nums[tail] == p.second;});
            int nindex = distance(it1,it2);
            vAns[1] = nindex+vAns[0];
        }
        else
        {
            vAns[1] = it2->first;
        }
        return vAns;
    }
};
```

Runtime: 4 ms
Memory Usage: 9.8 MB

經過排序後，效率還是第二個的3倍！
