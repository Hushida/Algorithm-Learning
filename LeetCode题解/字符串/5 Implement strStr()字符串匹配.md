## 题目描述：
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1

不能匹配就返回-1，成功匹配就返回匹配的第一个位置下标

思路：参考了讨论区代码  
双层循环，对于haystack的i位置，遍历找到和needle第一个字符相等的字符位置

通过的代码 
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.length() == 0) return 0; // edge case: "",""=>0  "a",""=>0
        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            for (int j = 0; j < needle.length() && haystack.charAt(i + j) == (needle.charAt(j)) ; j++)
                //包含了完整的needle字符串，返回起始位置
                if (j == needle.length() - 1) return i;
        }
        return -1;
    }
}
```
