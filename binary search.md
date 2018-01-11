---


---

<h1 id="chapter-1-binary-search">chapter 1 Binary search</h1>
<h3 id="一、模板">一、模板</h3>
<p>find the any/first/last position of target in nums
Time Complexity:</p>
<pre><code>O(1)
O(logn) binary search
O($ \sqrt{n}$ ) 分解质因数
O(n)高频
O(nlogn)排序
O($n^2$)数组，枚举，动态规划
O($n^3$)同上
O($2^n$)与组合有关的搜索
O(n!)与排列有关的搜索
</code></pre>
<p>template:</p>
<pre><code>while(start + 1 &lt; end)
</code></pre>
<p>即相邻就退出循环
example:
Last position of Target</p>
<pre><code>#错误：end = len(nums)-1, 别少了-1！！
def lastPosition(nums, target):
	if len(nums) == 0:
		return -1
	start = 0
	end = len(nums)-1
	while(start + 1 &lt; end):
		mid = start + (end - start)/2
		if nums[mid] &gt; target:
			end = mid
		else:
			start = mid
	if nums[end] == target:
		return end
	elif nums[start] == target:
		return start
	else:
		return -1	
</code></pre>
<h3 id="二、满足某个条件的第一个位置或者最后一个位置">二、满足某个条件的第一个位置或者最后一个位置</h3>
<p>例如数组中找到第一个/最后一个满足某一个条件的位置
OOOOOOOOXXXXX</p>
<p>Simple question:
Total occurrence of target in sorted array</p>
<pre><code>思路：找到第一个出现的target和最后出现的target
我的跑偏思路：找到最后一个
出现的比target小的以及第一个比target大的index
这样做很难处理 [1,1,1,1,1,1,1] 的情况
</code></pre>
<pre><code>def totalOccurrence(nums, traget):
	if len(nums) == 0:
		return 0
	start = 0
	end = len(nums) - 1
	while start + 1 &lt; end:
		mid = start + (end - start) / 2
		if nums[mid] &gt;= target:
			end = mid
		else:
			start = mid
	if nums[start] == target:
		begin = start
	elif nums[end] == target:
		begin = end
	else:
		return 0
	
	start = 0
	end = len(nums) - 1
	while start + 1 &lt; end:
		mid = start + (end - start) / 2
		if nums[mid] &gt; target:
			end = mid
		else:
			start = mid
	if nums[end] == target:
		last = end
	elif nums[start] == target:
		last = start
	else:
		return 0
	return last - begin + 1
</code></pre>
<p>Example 2:
Find the minimum element in rotated sorted array</p>
<p>思路：
看做xxoo的问题，即找到第一个比last element小的数</p>
<h3 id="三、理解二分，二分的本质是保留有解的一半，减少搜索空间。">三、理解二分，二分的本质是保留有解的一半，减少搜索空间。</h3>
<p>Example：Search in Rotated Sorted Array</p>
<p>思路：</p>

