---


---

<h2 id="chapter-7-array-and-two-pointersnote-from-jiuzhang">chapter 7 Array and Two pointers(note from jiuzhang)</h2>
<ol>
<li>Sorted Array</li>
</ol>
<p>Problem 1: merge two sorted array</p>
<pre><code>	 not in place 
	 思路：从头开始挨个比较，将小的删除并且加入新的数组里
</code></pre>
<pre><code>def MergeTwoarray(nums1, nums2):
	result = []
	while len(nums1) and len(nums2):
		if nums1[0] &lt;= nums2[0]:
			result.append(nums1.pop(0))
		else:
			result.append(nums2.pop(0))
	if len(nums1):
		result += nums1
	if len(nums2):
		result += nums2
	return result

</code></pre>
<p>Problem 2: merge sorted array</p>
<pre><code>	in place
	思路：从大头开始比较，往数组最后放，避免数组元素的移动
</code></pre>
<pre><code>def merge(nums1,m, nums2,n)
    length = m + n
    while m and n :
        if nums1[m-1] &gt;= nums2[n-1]:
            nums1[m+n-1] = nums1[m-1]
            m -= 1
        else:
            nums1[m+n-1] = nums2[n-1]
            n -= 1
    if m == 0:
        nums1[:n] = nums2[:n]
</code></pre>
<p>Problem 3: intersection of two arrays</p>
<pre><code>	思路：
	1 hash table 
	2 merge two sorted arrays, 先排序，从小比较，不同则弹出小的，相同则加入结果，去重
	3 binary search
</code></pre>
<ul>
<li>
<p>important problem : Median of two sorted array</p>
<pre><code>思路：最直观能想到的方法是类似于merge sorted array的方法，两个数组头对齐比较，弹出小的一方
知道弹出个数是两个数组元素之和的一半，这样做的时间复杂度是O(N)，是暴力解法
如果要优化的话，可以推测出本题时间复杂度应该是Log(n)，但是又很难想到有二分的解法，推测如下公式：

T(n) = T(n/2) + O(1)
本题转换思路，应变为找到two sorted array的第k个数，如果k= 两个数组元素数量之和的一半即为解。
我们要做的努力就是通过O(1)的时间将寻找第k个元素的任务变为寻找第k/2的任务，以此类推，即可得出logn的解法：

即比较两个数组的第k/2个数，弹出小的那一方的前k/2个数
因为假设我们按照merge sorted array一一比较弹出小的，到两个数组的第k/2个数的时候，弹出的最多是到所有数的第k-1个数，不会影响我们的解，所以直接去掉较小一方的前k/2个数是安全的并且将找到第k个数的问题降到找到第k/2个数的问题，以此继续降可变为K/4,K/8直到K变成1
</code></pre>
</li>
</ul>
<pre><code>class Solution(object):
   def findMedianSortedArrays(self, nums1, nums2):
       """
       :type nums1: List[int]
       :type nums2: List[int]
       :rtype: float
       """
       length = len(nums1) + len(nums2)
       if length % 2 == 0:
           return (self.findKth(nums1,nums2,length/2)+self.findKth(nums1,nums2,length/2+1))/ 2.0
       else:
           return self.findKth(nums1,nums2, (length+1)/2)*1.0
       
   def findKth(self, nums1, nums2, k):
       if len(nums1) == 0:
           return nums2[k-1]
       if len(nums2) == 0:
           return nums1[k-1]
       if k == 1:
           return min(nums1[0],nums2[0])
       if k/2 - 1 &lt; len(nums1):
           a = nums1[k/2-1]
       else:
           a = None
       if k/2 - 1 &lt; len(nums2):
           b = nums2[k/2-1]
       else:
           b = None
       if a == None or (b != None and a &gt; b):
           return self.findKth(nums1, nums2[k/2:],k - k/2)
       else:
           return self.findKth(nums1[k/2:], nums2, k - k/2)
</code></pre>

