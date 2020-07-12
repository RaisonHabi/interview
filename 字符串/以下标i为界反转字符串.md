### 注：本题未找到leetcode原题
## 大致描述
输入字符串和下标i，根据i把字符串划分前（不包含i）、后（包含i）两部分，互换前、后两部分。  
输入字符串以字符数组 char[] 的形式给出。  
不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

示例
```
i=3
['a','b','c','d','e']

['d','e','a','b','c']
```

&nbsp;
## 题解
思路：  
以i为界，前、后子串先反转，然后反转整个字符串
```
class Solution:
    def reverseString(self,i,s):
        if i==0 or i>len(s):return
        
        left,right=0,i-1
        while left<right:
            s[left],s[right]=s[right],s[left]
            left+=1
            right-=1
        left,right=i,len(s)-1
        while left<right:
            s[left],s[right]=s[right],s[left]
            left+=1
            right-=1
        left,right=0,len(s)-1
        while left<right:
            s[left],s[right]=s[right],s[left]
            left+=1
            right-=1
       
```

&nbsp;
