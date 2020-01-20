# 1122. Relative Sort Array

Given two arrays arr1 and arr2, the elements of arr2 are distinct, and all elements in arr2 are also in arr1.

Sort the elements of arr1 such that the relative ordering of items in arr1 are the same as in arr2.  

Elements that don't appear in arr2 should be placed at the end of arr1 in **ascending** order.

 

**Example 1:**

    Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
    Output: [2,2,2,1,4,3,3,9,6,7,19]
 

**Constraints:**

    *    arr1.length, arr2.length <= 1000
    *    0 <= arr1[i], arr2[i] <= 1000
    *    Each arr2[i] is distinct.
    *    Each arr2[i] is in arr1.
    
#### 題意:
輸入為兩個array,arr2中的每個元素不重複。arr1包含arr2的元素再加上其他元素

所需輸出為arr1 每個元素的排序如同arr2，若有沒出現在arr2的元素，則排在最末端並以**遞增**形式輸出。


#### 思路:

本題為easy等級，通常1~2個轉折就能解出答案。

利用arr2的性質來製表，再依hash值進行排序。

特別要注意的地方是-->arr1中沒出現在arr2的元素 該如何處理是本題重點。

那些在arr1卻沒在arr2中的元素必須遞增排列，所以我的作法是 當發現某元素沒在table時，手動賦hash值 = arr2.size + 該元素值

這樣就能遞增排列，並且和前面arr2中的元素錯開。

### 參考code:
```cpp
class Solution {
public:
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) 
    {
        unordered_map<int,int> mp;
        for(int i = 0; i<arr2.size();++i)
        {
            mp[arr2[i]] = i;
        }
        int arr2Size = arr2.size();
        sort(std::begin(arr1),std::end(arr1),[&mp,&arr2Size](int v1,int v2){
            if(mp.count(v1) == 0) mp[v1] = arr2Size+v1;
            if(mp.count(v2) == 0) mp[v2] = arr2Size+v2;
            return mp[v1] < mp[v2];
        });
        return arr1;
    }
};
```

Runtime: 8 ms  faster than 46.59% of C++ online submissions

Memory Usage: 9.2 MB less than 100.00% of C++ online submissions

粗估 time complexity為O(nlogn)
