---


---

<h2 id="find-min-in-rotated-sorted-array">153 Find Min in Rotated sorted Array</h2>
<ul>
<li>
<p>Question: Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.</p>
<p>(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2)<br>
Find the minimum element.<br>
You may assume no duplicate exists in the array.</p>
</li>
<li>
<p>Tag：Binary search，reduce the searching space of Min could be.即不断缩小最小值可能存在的搜索范围</p>
</li>
<li>
<p>Idea:  Set the last number of Array as target, if nums[mid] &gt; target, the Min element cannot be at the left of the mid, so we can reduce the space to [mid, end], otherwise, if nums[mid] &lt;= target, then the Min element must be at the left of the mid, so we can also reduce the space to [start, mid]</p>
</li>
<li>
<p>Time complexity: O(logn)</p>
</li>
<li>
<p>Space complexity: O(1)</p>
</li>
<li>
<p>Note: 1. Though we can use the <strong>first element</strong> of the array as the target in a rotated sorted array, but we have to know that <strong>A sorted array is a specific rotated sorted array</strong>, such as [1,2,3,4,5], but it will not work using the first element as target</p>
</li>
</ul>
<pre><code>PYTHON:
def findMin(nums):
	if len(nums) == 0:
		return None
	start = 0
	end = len(nums) - 1
	target = nums[-1]
	while start + 1 &lt; end:
		mid = start + (end - start)/2 // avoid stackoverflow
		if nums[mid] &lt;= target:
			end = mid
		else:
			start = mid
	if nums[start] &lt;= target:
		return nums[start]
	else:
		return nums[end]

</code></pre>

