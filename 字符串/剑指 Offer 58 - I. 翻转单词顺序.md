## 题目
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

示例 1：
```
输入: "the sky is blue"
输出: "blue is sky the"
```
示例 2：
```
输入: "  hello world!  "
输出: "world! hello"
```
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：
```
输入: "a good   example"
输出: "example good a"
```
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：  
无空格字符构成一个单词。  
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。  
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。  
注意：本题与主站 151 题相同：https://leetcode-cn.com/problems/reverse-words-in-a-string/

注意：此题对比原题有改动

&nbsp;
## 题解
方法一：双指针  
算法解析：  
倒序遍历字符串 s ，记录单词左右索引边界 i , j ；  
每确定一个单词的边界，则将其添加至单词列表 resres ；  
最终，将单词列表拼接为字符串，并返回即可。  
复杂度分析：
时间复杂度 O(N) ： 其中 N 为字符串 s 的长度，线性遍历字符串。
空间复杂度 O(N) ： 新建的 list(Python) 或 StringBuilder(Java) 中的字符串总长度 ≤N ，占用 O(N) 大小的额外空间。
```
class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip() # 删除首尾空格
        i = j = len(s) - 1
        res = []
        while i >= 0:
            while i >= 0 and s[i] != ' ': i -= 1 # 搜索首个空格
            res.append(s[i + 1: j + 1]) # 添加单词
            while s[i] == ' ': i -= 1 # 跳过单词间空格
            j = i # j 指向下个单词的尾字符
        return ' '.join(res) # 拼接并返回
```

&nbsp;
## reference
[面试题58 - I. 翻转单词顺序（双指针 / 库函数，清晰图解）](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/solution/mian-shi-ti-58-i-fan-zhuan-dan-ci-shun-xu-shuang-z/)
