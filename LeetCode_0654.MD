# 654. Maximum Binary Tree

You are given an integer array `nums` with no duplicates. A **maximum binary tree** can be built recursively from nums using the following algorithm:

Create a root node whose value is the maximum value in `nums`.
Recursively build the left subtree on the **subarray prefix** to the **left** of the maximum value.
Recursively build the right subtree on the **subarray suffix** to the **right** of the maximum value.
Return the ***maximum binary*** tree built from `nums`.

### Example 1:

![image](https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg)

    Input: nums = [3,2,1,6,0,5]
    Output: [6,3,5,null,2,0,null,null,1]
    Explanation: The recursive calls are as follow:
    - The largest value in [3,2,1,6,0,5] is 6. Left prefix is [3,2,1] and right suffix is [0,5].
        - The largest value in [3,2,1] is 3. Left prefix is [] and right suffix is [2,1].
            - Empty array, so no child.
            - The largest value in [2,1] is 2. Left prefix is [] and right suffix is [1].
                - Empty array, so no child.
                - Only one element, so child is a node with value 1.
        - The largest value in [0,5] is 5. Left prefix is [0] and right suffix is [].
            - Only one element, so child is a node with value 0.
            - Empty array, so no child.
            
### Example 2: 

![image](https://assets.leetcode.com/uploads/2020/12/24/tree2.jpg)

    Input: nums = [3,2,1]
    Output: [3,null,2,null,1]
    
### Constraints:

    1 <= nums.length <= 1000
    0 <= nums[i] <= 1000
    All integers in nums are unique.
    
## 思路:

乍看有點像快速排序的框架，找到數列最大值，再分兩半繼續插入樹

難得有bug free的一題，但效率就差了，有空再調看看
   
Runtime 204 ms  Beats 20.93%

Memory 52.8 MB Beats 20.49%

### 程式碼:

```cpp
class Solution {
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) 
    {
        if(nums.empty())
            return nullptr;
        int max = 0,pivot = 0;
        for(int i = 0;i<nums.size();++i)
        {
            if(nums[i]>max)
            {
                max = nums[i];
                pivot = i;
            }
        }
        TreeNode* root = new TreeNode(max);
        vector<int> left_part(nums.begin(),nums.begin()+pivot);
        vector<int> right_part(nums.begin()+pivot+1,nums.end());
        root->left = constructMaximumBinaryTree(left_part);
        root->right = constructMaximumBinaryTree(right_part);
        return root;
    }
};
```
