# 215. Kth Largest Element in an Array


Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

#### Example 1:

    Input: [3,2,1,5,6,4] and k = 2
    Output: 5

#### Example 2:

    Input: [3,2,3,1,2,4,5,5,6] and k = 4
    Output: 4
Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.

#### 解題想法：

複習quick sort的一題

很智障的解法是直接用sort排好後再把k挑出來

但更智障的是，自己刻的快排效率還差了不少...

講回來，核心概念是將function分成partition和主程式

partition return一個經過快排後的中間index

再利用此值來判斷k會落在哪裡，若index == k-1

找到此值直接return 


```cpp
class Solution 
{
public:
    int findKthLargest(vector<int>& nums, int k) 
    {
        int right = nums.size()-1;
        int left = 0;
        int ans = 0;
        while(true)
        {
            int pivot = partition(nums,left,right);
            if(k-1 == pivot)
            {
                ans = nums[pivot];
                break;
            }
            if(k-1 > pivot)
            {
                left = pivot+1;
            }
            else
                right = pivot-1;
        }
         // quickSort(nums,0,nums.size()-1);
         // for(auto& num :nums)
         //     cout<<num<<" ";
        
        return ans;
    }
    
    void quickSort(vector<int>& nums,int left,int right)
    {
        if(left<right)
        {
            int pos = partition(nums,left,right);
            quickSort(nums,left,pos-1);
            quickSort(nums,pos+1,right);
        }
    }
    
    int partition(vector<int>& nums,int left,int right)
    {
        int length = nums.size();
        int pivot = nums[right];
        int index = left-1,j = right;
        while(true)
        {
            while(index+1<length && nums[++index]>pivot);
            while(j-1>=0 && nums[--j]<pivot);
            
            if(index>=j)
                break;
            swap(nums[index],nums[j]);
        }
        swap(nums[index],nums[right]);
        return index;
    }
    
};
```

出的很棒的一題，有空再把python版的補上 

思路很簡單，反倒是花很多時間再複習快排...

參考資料:https://www.cnblogs.com/grandyang/p/4539757.html

https://openhome.cc/Gossip/AlgorithmGossip/QuickSort1.htm#Python

https://openhome.cc/Gossip/AlgorithmGossip/QuickSort2.htm

https://openhome.cc/Gossip/AlgorithmGossip/QuickSort3.htm
