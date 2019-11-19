# 34. Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

**Example 1:**

    Input: nums = [5,7,7,8,8,10], target = 8
    Output: [3,4]
    
**Example 2:**    

    Input: nums = [5,7,7,8,8,10], target = 6
    Output: [-1,-1]

#### 思路:

題目要求time complexity在O(log n)以內完成，

可以推斷出要在低於一個迴圈內的時間找到答案，這時可以先想到雙指標(index)

但我第一次刷時居然是先想到用std::find 來計算

由於find運作在random access container時複雜度會比線性低

即便做兩次find，最後結果仍和雙指標的做法相差無幾

而且程式碼精簡許多，只是要處理反向iterator轉成正向

使用.base() 記得要-1

#### 參考code:

1. 雙指標
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) 
    {        
        if(nums.empty())
            return {-1,-1};
        int head = 0,tail = nums.size()-1;
        vector<int> vAns(2,-1);
        if(nums.size()<2 && target == nums[0])
        {
            vAns[0] = 0;
            vAns[1] = 0;
        }
        while(head <= tail)
        {
            if(nums[head]<target)
            {
                head++;
            }
            else if(nums[tail]>target)
            {
                tail--;
            }
            else if(nums[tail] == nums[head])
            {
                vAns[0] = head;
                vAns[1] = tail;
                break;
            }
        }
        return vAns;
    }
};
```

2. find法
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) 
    {
        vector<int> vAns(2,-1);
        auto it1 = find(nums.begin(),nums.end(),target);
        if(it1 == nums.end())
            return vAns;
        vAns[0] = distance(nums.begin(),it1);
        auto it2 = find(nums.rbegin(),nums.rend(),target);
        vAns[1] = distance(nums.begin(),it2.base())-1;
        
        return vAns;
    }
};
```

Runtime: 8 ms, faster than 85.18%

Memory Usage: 10.2 MB, less than 97.80%

兩個做法時間都差不多
