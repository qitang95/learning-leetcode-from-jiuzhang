---


---

<h2 id="search-in-rotated-sorted-array">33 Search in Rotated sorted Array</h2>
<ul>
<li>
<p>Question: Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.<br>
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).<br>
You are given a target value to search. If found in the array return its index, otherwise return -1.<br>
You may assume no duplicate exists in the array.</p>
</li>
<li>
<p>Tag: Binary Search</p>
</li>
<li>
<p>Idea: Try to think about three numbers: nums[mid], target, and nums[-1]( The reason why use nums[-1] can be found in <strong>Leetcode 153</strong>), there are two big situation: nums[mid] &gt; nums[-1] and nums[mid] &lt;= nums[-1], take the former as an example, the target can located in three different location:<br>
- nums[-1] &lt; target &lt; nums[mid]<br>
-  target &lt;= nums[-1]<br>
- target &gt; nums[mid]<br>
the last two are the same, we can reduce the space to [mid, end]<br>
and for the first one we can reduce the space to [start, mid]</p>
</li>
<li>
<p>Time complexity: O(logn)</p>
</li>
<li>
<p>Space complexity: O(1)</p>
</li>
<li>
<p>Note: When compare target and nums[-1], we should be careful about the ‘=’, when nums[mid] &gt; nums[-1] and nums[-1] == target, we should let start = mid, however, when nums[mid] &lt;= nums[-1] and nums[-1] == target, we should let start = mid too.</p>
</li>
</ul>
<pre><code>PYTHON:
def search(nums, target):
	if len(nums) == 0:
		return -1
	start = 0
	end = len(nums) - 1
	while start + 1 &lt; end:
		mid = start + (end - start) /2
		if nums[mid] == target:
			return mid
		elif nums[mid] &gt; nums[-1]:
			if target &gt; nums[-1] and target &lt; nums[mid]:
				end = mid
			else:
				start = mid
		else:
			if target &lt;= nums[-1] and target &gt; nums[mid]:
				start = mid
			else:
				end = mid
	if nums[start] == target:
			return start
	if nums[end] == target:
			return end
	return -1
 
</code></pre>

