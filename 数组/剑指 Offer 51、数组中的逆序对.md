## 题目
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。
```
示例 1:

输入: [7,5,6,4]
输出: 5
 
限制：
0 <= 数组长度 <= 50000
```

&nbsp;
## 题解
### 方法一：归并排序
#### 预备知识
「归并排序」是分治思想的典型应用，它包含这样三个步骤：
```
分解： 待排序的区间为 [l, r]，令 m = (l+r)/2，我们把 [l, r] 分成 [l, m] 和 [m + 1, r]
解决： 使用归并排序递归地排序两个子序列
合并： 把两个已经排好序的子序列 [l, m] 和 [m + 1, r] 合并起来
```
在待排序序列长度为 1 的时候，递归开始「回升」，因为我们默认长度为 1 的序列是排好序的。

#### 思路
......
```
class Solution:
    def mergeSort(self, nums, tmp, l, r):
        if l >= r:
            return 0

        mid = (l + r) // 2
        inv_count = self.mergeSort(nums, tmp, l, mid) + self.mergeSort(nums, tmp, mid + 1, r)
        i, j, pos = l, mid + 1, l
        while i <= mid and j <= r:
            if nums[i] <= nums[j]:
                tmp[pos] = nums[i]
                i += 1
                inv_count += (j - (mid + 1))
            else:
                tmp[pos] = nums[j]
                j += 1
            pos += 1
        for k in range(i, mid + 1):
            tmp[pos] = nums[k]
            inv_count += (j - (mid + 1))
            pos += 1
        for k in range(j, r + 1):
            tmp[pos] = nums[k]
            pos += 1
        nums[l:r+1] = tmp[l:r+1]
        return inv_count

    def reversePairs(self, nums: List[int]) -> int:
        n = len(nums)
        tmp = [0] * n
        return self.mergeSort(nums, tmp, 0, n - 1)
```
链接：https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/solution/shu-zu-zhong-de-ni-xu-dui-by-leetcode-solution/

#### 复杂度
记序列长度为 n。   
时间复杂度：同归并排序 O(nlogn)。
空间复杂度：同归并排序 O(n)，因为归并排序需要用到一个临时数组。
### 方法二：离散化树状数组
......

&nbsp;
## reference
[剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)
