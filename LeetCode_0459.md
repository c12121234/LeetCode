# 459. Repeated Substring Pattern

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. 

You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

 

**Example 1:**

    Input: "abab"
    Output: True
    Explanation: It's the substring "ab" twice.

**Example 2:**

    Input: "aba"
    Output: False

**Example 3:**

    Input: "abcabcabcabc"
    Output: True
    Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
    

## 題意:

若字串s可為子字串組成，返回True 反之False

## 思路:

直覺暴力法，後來查了下還有更好的解法，之後來試試看

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        for index,value in enumerate(s):
            str_temp_text = s[:index+1]
            if str_temp_text == s:
                break
            temp_list = s.split(str_temp_text)
            answer_set = set(temp_list)
            if len(answer_set) == 1:
                return True
        return False
``` 

Runtime: **3820 ms**, faster than **5.00%** of Python3 online submissions for Repeated Substring Pattern.

Memory Usage: 14.5 MB, less than **26.42%** of Python3 online submissions for Repeated Substring Pattern.

爛的很好笑...
