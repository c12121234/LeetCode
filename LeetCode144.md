# 144. Binary Tree Preorder Traversal

Given a binary tree, return the preorder traversal of its nodes' values.

**Example:**

    Input: [1,null,2,3]
       1
        \
         2
        /
       3
    
    Output: [1,2,3]
    
**Follow up:** Recursive solution is trivial, could you do it iteratively?

#### 思路

Preorder,Inorder,postorder樹的走訪問題
很單純的使用遞迴或stack來解

要留心的就是levelorder要用queue來解就是了
easy

#### 參考code
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) 
    {
        if(root == nullptr)
            return {};
        vector<int> vAns;
        stack<TreeNode*> stk;
        stk.push(root);
        while(!stk.empty())
        {
            TreeNode* pTop = stk.top();
            vAns.push_back(pTop->val);                        
            stk.pop();
            if(pTop->right)
                stk.push(pTop->right);
            if(pTop->left)
                stk.push(pTop->left);            
        }
        return vAns;
    }
};
```

Runtime: 4 ms, faster than 59.04%

Memory Usage: 9.1 MB, less than 100.00%
