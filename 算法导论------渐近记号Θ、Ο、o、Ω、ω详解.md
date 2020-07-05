##  渐进记号
### 1.渐近紧确界记号： $Θ$（big-theta）
Θ记号在五个记号中，要求是最严格的，因为g(n)即可以表示上界也可以表示下界。

### 2.渐近上界记号：$O$(big-oh)
根据符号O的定义，用它评估算法的复杂度得到的只是问题规模充分大时的一个上界。这个上界的阶越低，评估越精确，越有价值。

几种常见的复杂度关系
```
O(1)<O(log(n))<O(n)<O(nlogn)<O(n^2)<O(2^n)<O(n!)<O(n^n)
需要注意的是：对数函数在没有底数时，默认底数为2；如lgn=logn=log2n
因为计算机中很多程序是用二分法实现的。
```

### 3.渐近下界记号：$Ω$(big-omege)

### 4.非渐近紧确上界：o(小-oh)

### 5.非渐近紧确下界：ω(小-omege)

### 6.渐近记号Θ、Ο、o、Ω、ω关系
<table>
<thead>
<tr>
<th>记号</th>
<th>含义</th>
<th>通俗理解</th>
</tr>
</thead>
<tbody>
<tr>
<td>(1)Θ（西塔）</td>
<td>紧确界。</td>
<td>相当于"="</td>
</tr>
<tr>
<td>(2)O （大欧）</td>
<td>上界。</td>
<td>相当于"&lt;="</td>
</tr>
<tr>
<td>(3)o（小欧）</td>
<td>非紧的上界。</td>
<td>相当于"&lt;"</td>
</tr>
<tr>
<td>(4)Ω（大欧米伽）</td>
<td>下界。</td>
<td>相当于"&gt;="</td>
</tr>
<tr>
<td>(5)ω（小欧米伽）</td>
<td>非紧的下界。</td>
<td>相当于"&gt;"</td>
</tr>
</tbody>
</table><p><img src="https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYxMTI2MjE0OTM0NTk4?x-oss-process=image/format,png" alt="在这里插入图片描述"></p>
<hr>

&nbsp;

## 上界
上界（upper bound）是一个与偏序集有关的特殊元素，指的是偏序集中大于或等于它的子集中一切元素的元素。若数集S为实数集R的子集有上界，则显然它有无穷多个上界，而其中最小的一个上界常常具有重要的作用，称它为数集S的上确界。

&nbsp;
## reference
[算法导论------渐近记号Θ、Ο、o、Ω、ω详解](https://blog.csdn.net/so_geili/article/details/53353593)  
[上确界](https://baike.baidu.com/item/%E4%B8%8A%E7%A1%AE%E7%95%8C) 
