# 105. Construct Binary Tree from Preorder and Inorder Traversal

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

    preorder = [3,9,20,15,7]
    inorder = [9,3,15,20,7]
Return the following binary tree:

        3
       / \
      9  20
        /  \
       15   7
       

## 思路
* 1. preorder第一個必為root
* 2. 找出root在inorder中的位置
* 3. 在inorder中，root之前的皆為左子樹
* 4. 在inorder中，root之後的皆為右子樹
* 5. 利用遞迴實作(或iterator ?)

以下參考code:

```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) 
    {
        return divConquer(preorder,inorder,0,preorder.size()-1,0,inorder.size()-1);
    }
private:
    TreeNode* divConquer(vector<int>& pre,vector<int>& in,int pl,int pr,int il,int ir)
    {
        if(pl > pr)
            return nullptr;
        TreeNode* pRoot = new TreeNode(pre[pl]);
        for(int i = il; i<=ir;++i)
        {
            if(pre[pl] == in[i])
            {
                pRoot->left = divConquer(pre,in,pl+1,pl+(i-il),il,i-1);
                pRoot->right = divConquer(pre,in,pl+(i-il)+1,pr,i+1,ir);
            }
        }
        return pRoot;
    }
};

```

Runtime: 24 ms, faster than 35.46%

Memory Usage: 16.7 MB, less than 71.43%

差強人意阿...
