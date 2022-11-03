# 450. Delete Node in a BST


Given a root node reference of a BST and a key, delete the node with the given key in the BST. **Return the root node reference** *(possibly updated) of the BST.*

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Example 1:**

![image](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

    Input: root = [5,3,6,2,4,null,7], key = 3
    Output: [5,4,6,2,null,null,7]
    Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
    One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
    Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.

![image](https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg)


**Example 2:**

    Input: root = [5,3,6,2,4,null,7], key = 0
    Output: [5,3,6,2,4,null,7]
    Explanation: The tree does not contain a node with value = 0.
    
**Example 3:**

    Input: root = [], key = 0
    Output: []
    
**Constraints:**

    The number of nodes in the tree is in the range [0, 10^4].
    -10^5 <= Node.val <= 10^5
    Each node has a unique value.
    root is a valid binary search tree.
    -10^5 <= key <= 10^5


## 解題思路:

思考刪除節點的所有情形(刪除leaf,刪除root,刪除有單一child,刪除有兩個child)

要維持BST形式，刪除的節點必須由左子樹中最大的子節點或右子樹中最小子節點代替

兩種思考方式皆可，此處我用右子樹最小節點

## 程式碼:

```cpp
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) 
    {
        if(!root)
            return nullptr;
        if(root->val == key)
        {
            if(!root->left) return root->right;
            if(!root->right) return root->left;
            
            TreeNode* node=getMinNode(root->right);
            root->right=deleteNode(root->right,node->val);
            node->left = root->left;
            node->right = root->right;
            root = node;
        }
        else if(root->val>key)
            root->left=deleteNode(root->left,key);
        else if(root->val<key)
            root->right=deleteNode(root->right,key);
        return root;
    }
private:
    TreeNode* getMinNode(TreeNode* root)
    {
        while(root->left)
            root=root->left;
        return root;
    }
};
```


Runtime: 35 ms, faster than 95.67% of C++ online submissions for Delete Node in a BST.
Memory Usage: 32.7 MB, less than 42.81% of C++ online submissions for Delete Node in a BST.
