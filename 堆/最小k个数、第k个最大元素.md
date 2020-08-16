优化：1.k是否小于len/2；2.全部堆排序改为k个元素排序？

考察点：
```
1.快排的实现，快排的优化；
2.堆的手动实现
```
[二叉堆详解实现优先级队列](https://labuladong.github.io/ebook/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E7%B3%BB%E5%88%97/%E4%BA%8C%E5%8F%89%E5%A0%86%E8%AF%A6%E8%A7%A3%E5%AE%9E%E7%8E%B0%E4%BC%98%E5%85%88%E7%BA%A7%E9%98%9F%E5%88%97.html)

&nbsp;
## 题目1
[面试题 17.14. 最小K个数](https://leetcode-cn.com/problems/smallest-k-lcci/)

设计一个算法，找出数组中最小的k个数。以任意顺序返回这k个数均可。

示例：
```
输入： arr = [1,3,5,7,2,4,6,8], k = 4
输出： [1,2,3,4]
```
提示：
```
0 <= len(arr) <= 100000
0 <= k <= min(100000, len(arr))
```

&nbsp;
### 1.最大堆解法一(手动维护堆！面试考察)
```
    public int[] smallestK(int[] arr, int k) {
        int len = arr.length;
        if (k >= len) {
            return arr;
        }

        buildMinHeap(arr, len);

        int pos = len - k;
        for (int i = len - 1; i >= pos; i--) {
            swap(arr, 0, i);
            heapify(arr, 0, --len);
        }

        int[] ret = new int[k];
        System.arraycopy(arr, pos, ret, 0, k);
        return ret;
    }

    private void buildMinHeap(int[] arr, int len) {
        for (int i = (len - 1) / 2; i >= 0; i--) {
            heapify(arr, i, len);
        }
    }

    private void heapify(int[] arr, int i, int len) {
        if (i >= len) return;

        int min = i;
        int c1 = 2 * i + 1;
        int c2 = 2 * i + 2;

        if (c1 < len && arr[c1] < arr[min]) {
            min = c1;
        }
        if (c2 < len && arr[c2] < arr[min]) {
            min = c2;
        }

        if (min != i) {
            swap(arr, i, min);
            heapify(arr, min, len);
        }
    }

    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }

```
链接：https://leetcode-cn.com/problems/smallest-k-lcci/solution/javashou-si-kuai-pai-dui-pai-by-qrqhuang-2/

### 2.最大堆解法二
思路：堆排序 复杂度O(nlogk)
```
1.遍历输入数组，将前k个数插入到推中；

2.继续从输入数组中读入元素做为待插入整数，并将它与堆中最大值比较：
如果待插入的值比当前已有的最大值小，则用这个数替换当前已有的最大值；如果待插入的值比当前已有的最大值还大，则抛弃这个数，继续读下一个数。
这样动态维护堆中这k个数，以保证它只储存输入数组中的前k个最小的数，最后输出堆即可。
```
链接：https://leetcode-cn.com/problems/smallest-k-lcci/solution/li-yong-dui-pai-xu-by-yi-mi-yuan-de-tian-tang/

```
import heapq
class Solution:
    def smallestK(self, arr: List[int], k: int) -> List[int]:
        if k>len(arr) or k==0:
            return []
        heap = []
        for i in arr[:k]:
            heapq.heappush(heap, -i)   ##### hepq是最小堆，加负号即变为最大堆
        for i in arr[k:]:
            if i < -heap[0]:
                heapq.heappop(heap)
                heapq.heappush(heap, -i)
        result = []
        for i in range(k):
            result.append(-heapq.heappop(heap))
        return result[::-1]
```

python3.8.5:  
这个模块提供了堆队列算法的实现，也称为优先队列算法    
这在教材中称为“最小堆”     
基于这两方面，把堆看作原生的Python list也没什么奇怪的： heap[0] 表示最小的元素，同时 heap.sort() 维护了堆的不变性！    
[heapq --- 堆队列算法](https://docs.python.org/zh-cn/3/library/heapq.html)
### 3.快排解法一
```
###以中间的数作为基准数
class Solution:
    def smallestK(self, arr: List[int], k: int) -> List[int]:
        def quicksort(s):
            if len(s)<2:
                return s
            mid=s[len(s)//2]
            s.remove(mid)
            l=[]
            r=[]
            for i in range(len(s)):
                if s[i]<=mid:
                    l.append(s[i])
                else:
                    r.append(s[i])
            return quicksort(l)+[mid]+quicksort(r)
        a=quicksort(arr)
        return a[:k]
```
链接：https://leetcode-cn.com/problems/smallest-k-lcci/solution/ben-ti-kao-de-shi-pai-xu-ti-by-jamiechen_sjtu/

### 4.快排解法二
```
    public int[] smallestK(int[] arr, int k) {
        if (k >= arr.length) {
            return arr;
        }

        int low = 0;
        int high = arr.length - 1;
        ###取到前k小个数
        while (low < high) {
            int pos = partition(arr, low, high);
            if (pos == k - 1) {
                break;
            } else if (pos < k - 1) {
                low = pos + 1;
            } else {
                high = pos - 1;
            }
        }

        int[] dest = new int[k];
        System.arraycopy(arr, 0, dest, 0, k);
        return dest;
    }

###以第一个数作为基准数
    private int partition(int[] arr, int low, int high) {
        int pivot = arr[low];
        while (low < high) {
            while (low < high && arr[high] >= pivot) {
                high--;
            }

            arr[low] = arr[high];
            while (low < high && arr[low] <= pivot) {
                low++;
            }
            arr[high] = arr[low];
        }
        arr[low] = pivot;
        return low;
    }
```
链接：https://leetcode-cn.com/problems/smallest-k-lcci/solution/javashou-si-kuai-pai-dui-pai-by-qrqhuang-2/   

### 附：快排代码
```
void quicksort(int a[], int left, int right) {
    int i, j, t, privotkey;
    if (left > right)   //（递归过程先写结束条件）
        return;
 
    privotkey = a[left]; //temp中存的就是基准数（枢轴）
    i = left;
    j = right;
    while (i < j) {
        //顺序很重要，要先从右边开始找（最后交换基准时换过去的数要保证比基准小，因为基准选取数组第一个数）
        while (a[j] >= privotkey && i < j) {
            j--;
        }
        a[i] = a[j];
        //再找左边的
        while (a[i] <= privotkey && i < j) {
            i++;
        }
        a[j] = a[i];
    }
    //最终将基准数归位
    a[i] = privotkey;
 
    quicksort(a, left, i - 1);//继续处理左边的，这里是一个递归的过程
    quicksort(a, i + 1, right);//继续处理右边的 ，这里是一个递归的过程
}
```
[白话经典算法系列之六 快速排序 快速搞定](https://blog.csdn.net/MoreWindows/article/details/6684558)   
[排序算法时间复杂度、空间复杂度、稳定性比较](https://blog.csdn.net/pange1991/article/details/85460755)

### 附2:快排最好、最坏情况
在最优情况下，Partition每次都划分得很均匀，如果排序n个关键字，其递归树的深度就为.log2n.+1（.x.表示不大于x的最大整数），即仅需递归log2n次，需要时间为T（n）的话，第一次Partiation应该是需要对整个数组扫描一遍，做n次比较。然后，获得的枢轴将数组一分为二，那么各自还需要T（n/2）的时间（注意是最好情况，所以平分两半）。于是不断地划分下去，我们就有了下面的不等式推断。

也就是说，在最优的情况下，快速排序算法的时间复杂度为O(nlogn)。

在最坏的情况下，待排序的序列为正序或者逆序，每次划分只得到一个比上一次划分少一个记录的子序列，注意另一个为空。如果递归树画出来，它就是一棵斜树。此时需要执行n‐1次递归调用，且第i次划分需要经过n‐i次关键字的比较才能找到第i个记录，也就是枢轴的位置，因此比较次数为

，最终其时间复杂度为O(n2)。

平均的情况，设枢轴的关键字应该在第k的位置（1≤k≤n），那么：   
由数学归纳法可证明，其数量级为O(nlogn)。

[快速排序最好，最坏，平均复杂度分析](https://blog.csdn.net/weshjiness/article/details/8660583)

&nbsp;
## 题目2
[]()
### 1.基于堆排序的选择方法
思路和算法:  
我们也可以使用堆排序来解决这个问题——建立一个大根堆，做 k−1 次删除操作后堆顶元素就是我们要找的答案。  
在很多语言中，都有优先队列或者堆的的容器可以直接使用，但是在面试中，面试官更倾向于让更面试者自己实现一个堆。  
所以建议读者掌握这里大根堆的实现方法，在这道题中尤其要搞懂「建堆」、「调整」和「删除」的过程。

链接：https://leetcode-cn.com/problems/kth-largest-element-in-an-array/solution/shu-zu-zhong-de-di-kge-zui-da-yuan-su-by-leetcode-/

### 2.快排优化
注意：随机化pivot避免极端测试用例

partition（切分）操作总能排定一个元素，还能够知道这个元素它最终所在的位置，这样每经过一次 partition（切分）操作就能缩小搜索的范围，这样的思想叫做 “减而治之”（是 “分而治之” 思想的特例）
```
from typing import List
import random


class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        size = len(nums)

        target = size - k
        left = 0
        right = size - 1
        while True:
            index = self.__partition(nums, left, right)
            if index == target:
                return nums[index]
            elif index < target:
                # 下一轮在 [index + 1, right] 里找
                left = index + 1
            else:
                right = index - 1

    #  循环不变量：[left + 1, j] < pivot
    #  (j, i) >= pivot
    def __partition(self, nums, left, right):

        pivot = nums[left]
        j = left
        for i in range(left + 1, right + 1):
            if nums[i] < pivot:
                j += 1
                nums[i], nums[j] = nums[j], nums[i]

        nums[left], nums[j] = nums[j], nums[left]
        return j
```
链接：https://leetcode-cn.com/problems/kth-largest-element-in-an-array/solution/partitionfen-er-zhi-zhi-you-xian-dui-lie-java-dai-/

&nbsp;
## reference
[面试题 17.14. 最小K个数](https://leetcode-cn.com/problems/smallest-k-lcci/)
