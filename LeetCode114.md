# 114. Flatten Binary Tree to Linked List

Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

         1
        / \
       2   5
      / \   \
     3   4   6

The flattened tree should look like:

    1
     \
      2
       \
        3
         \
          4
           \
            5
             \
              6

## 思路
* 1. 將所有左節點轉移至右節點
* 2. 找出該左子樹中最大的節點(即該子樹最右下方的節點)
* 3. 將右子樹連接到左子樹中最大節點
* 4. 將左子樹轉移至右子樹(assign)
* 5. 將左子樹給予null
* 6. 進行至下一節點(右節點)

```cpp
    class Solution {
    public:
        void flatten(TreeNode* root) 
        {
            TreeNode* pCurr = root;
            while(pCurr)
            {
                if(pCurr->left)
                {
                    TreeNode* pTempLeft = pCurr->left;
                    while(pTempLeft->right)
                        pTempLeft = pTempLeft->right;
                    pTempLeft->right = pCurr->right;
                    pCurr->right = pCurr->left;
                    pCurr->left = nullptr;
                }
                pCurr = pCurr->right;
            }
        }
    };
```

Runtime: 8 ms,
faster than 54.30%

Memory Usage: 9.5 MB, less than 100.00%

**還是有地方可以加強的吧**
