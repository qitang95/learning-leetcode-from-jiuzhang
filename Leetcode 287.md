---


---

<h2 id="find-the-duplicate-number">287  Find the Duplicate Number</h2>
<ul>
<li>
<p>Question: Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.<br>
Note:<br>
You must not modify the array (assume the array is read only).<br>
You must use only constant, O(1) extra space.<br>
Your runtime complexity should be less than O(n2).<br>
There is only one duplicate number in the array, but it could be repeated more than once.</p>
</li>
<li>
<p>Tag: Binary Search, Two pointers,</p>
</li>
<li>
<p>Idea:</p>
<ol>
<li>The basic idea should be sort, we can only check the next number in the array and and get the answer in O(n) time after sorting, but sorting takes O(nlogn) time, so the total time complexity is O(nlogn).</li>
<li>But it needs modifying the array, which don’t match the request. So we can also use <strong>Set</strong> to solve the problem, we can put the number of array it a set, and then check whether 1-N in this set and get the answer. Time complexity: O(n) and Space complexity is O(n).</li>
<li>What if we have to use constant space? So we can use binary search to solve it. You may ask if not sorted, why binary search, we have to remember that binary search can be used when we can reduce the searching space and remains can be seen as the same structure as the original. So maybe we can check whether the value of the answer in [1,n/2] or in [n/2, n], we can count the number in the array that smaller than the middle value. If the count is smaller, which means the value of duplicate must be at [n/2,n], otherwise, at[1,n/2]. Time complexity: O(nlogn) and Space complexity is O(1).</li>
</ol>
</li>
<li>
<p>Note: there is another solution called Floyd’s Tortoise and Hare, which can be used to detect the cycle in Linked-list, which is better, Time complexity: O(n) and Space complexity is O(1). I will update the algorithm after learning.</p>
</li>
</ul>
<pre><code>PYTHON:
def findDuplicate(nums):
	if len(nums) == 0:
		return -1
	start = 1
	end =  len(nums) - 1       ##n
	while start + 1 &lt; end:
		count = 0
		mid = start + (end - start)/2
		for i in nums:
			if i &lt; mid:
				count += 1
		if count &lt; mid:
			start = mid
		else:
			end = mid
	count = 0
	for i in nums:
		if i == start:
			count += 1
	if count &gt; 1:
		return start
	else:
		return end
				
	
</code></pre>

