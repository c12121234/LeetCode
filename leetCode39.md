# 39. Combination Sum

Given a **set** of candidate numbers (candidates) **(without duplicates)** and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The **same** repeated number may be chosen from candidates unlimited number of times.

**Note:**

* All numbers (including target) will be positive integers.

* The solution set must not contain duplicate combinations.

**Example 1:**

    Input: candidates = [2,3,6,7], target = 7,
    A solution set is:
    [
      [7],
      [2,2,3]
    ]
    
**Example 2:**

    Input: candidates = [2,3,5], target = 8,
    A solution set is:
    [
      [2,2,2,2],
      [2,3,3],
      [3,5]
    ]

#### 思路:

當需要列出**所有**組合時，應該優先以回溯法來考慮

而回溯法要考慮的是: 1. 迭代的條件(分支) 2. 跳出迭代的條件 3. 邊界條件

而這題，可以先最佳化數列(排序)，這樣在判斷上會比較方便

此題的元素可以重複使用，因此該用一索引值紀錄目前使用的元素


#### 參考code:

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) 
    {   
        sort(candidates.begin(),candidates.end());
        vector<vector<int>> vvAns;
        vector<int> vTemp;
        BackTrace(vvAns,vTemp,target,candidates,0);
        return vvAns;
    }
private:
    void BackTrace(vector<vector<int>>& vvAns,vector<int>& vTemp,
                   int target,vector<int>& cadidates,int index)
    {
        if(target < 0)
            return;
        else if(target == 0)
        {
            vvAns.push_back(vTemp);
            return;
        }
        else
        {
            for(int i = index; i<cadidates.size();++i)
            {
                vTemp.push_back(cadidates[i]);
                BackTrace(vvAns,vTemp,target-cadidates[i],cadidates,i);
                vTemp.pop_back();
            }
        }
    }

};
```

Runtime: 12 ms, faster than 83.34%

Memory Usage: 9.2 MB, less than 100.00%

