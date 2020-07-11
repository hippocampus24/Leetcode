<!-- GFM-TOC -->
* [1. 把数组中的 0 移到末尾](#1-把数组中的-0-移到末尾)
* [2. 改变矩阵维度](#2-改变矩阵维度)
* [3. 找出数组中最长的连续 1](#3-找出数组中最长的连续-1)
* [4. 有序矩阵查找](#4-有序矩阵查找)
* [5. 有序矩阵的 Kth Element](#5-有序矩阵的-kth-element)
* [6. 一个数组元素在 [1, n] 之间，其中一个数被替换为另一个数，找出重复的数和丢失的数](#6-一个数组元素在-[1,-n]-之间，其中一个数被替换为另一个数，找出重复的数和丢失的数)
* [7. 找出数组中重复的数，数组值在 [1, n] 之间](#7-找出数组中重复的数，数组值在-[1,-n]-之间)
* [8. 数组相邻差值的个数](#8-数组相邻差值的个数)
* [9. 数组的度](#9-数组的度)
* [10. 对角元素相等的矩阵](#10-对角元素相等的矩阵)
* [11. 嵌套数组](#11-嵌套数组)
* [12. 分隔数组](#12-分隔数组)
<!-- GFM-TOC -->


# 1. 把数组中的 0 移到末尾

283\. Move Zeroes (Easy)

[力扣](https://leetcode-cn.com/problems/move-zeroes/description/)

```html
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。
```


讲解：[Youtube](https://www.youtube.com/watch?v=3gPn77w8ezw)


```python
class Solution(object):
	def moveZeroes(self, nums):
		"""
		:type nums: List[int]
		:rtype: None Do not return anything, modify nums in-place instead.
		"""
		if not nums:
			return 0
		# 第一次遍历的时候，j指针记录非0的个数，只要是非0的统统都赋给nums[j]	
		j = 0
		for i in range(len(nums)):
			if nums[i]:
				nums[j] = nums[i]
				j += 1
		# 非0元素统计完了，剩下的都是0了
		# 所以第二次遍历把末尾的元素都赋为0即可
		for i in range(j,len(nums)):
			nums[i] = 0
```

# 2. 改变矩阵维度

566\. Reshape the Matrix (Easy)

[力扣](https://leetcode-cn.com/problems/reshape-the-matrix/description/)

```html
Input:
nums =
[[1,2],
 [3,4]]
r = 1, c = 4

Output:
[[1,2,3,4]]

Explanation:
The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
```

```html
讲解：[Youtube](https://www.youtube.com/watch?v=3gPn77w8ezw)  
```

```python
class Solution:
    def matrixReshape(self, nums: List[List[int]], r: int, c: int) -> List[List[int]]:
        m,n=len(nums),len(nums[0])
        if m*n!=r*c:
            return nums
        res=[i for j in nums for i in j]    
        return [res[i:i+c] for i in range(0,len(res),c)]
```

# 3. 找出数组中最长的连续 1

485\. Max Consecutive Ones (Easy)

[力扣](https://leetcode-cn.com/problems/max-consecutive-ones/description/)

```html
讲解：https://www.youtube.com/watch?v=Ou7y2YZEQxg
```

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        count = 0
        max_count = 0
        for num in nums:
            if num == 1:
                # Increment the count of 1's by one.
                count += 1
            else:
                # Find the maximum till now.
                max_count = max(max_count, count)
                # Reset count of 1.
                count = 0
        return max(max_count, count)
```

# 4. 有序矩阵查找

240\. Search a 2D Matrix II (Medium)

[力扣](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/description/)

```html
[
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
]
```

讲解：[Youtube](https://www.youtube.com/watch?v=g4Qy83toSzc)
    

```python
class Solution:
    def binary_search(self, matrix, target, start, vertical):
        lo = start
        hi = len(matrix[0])-1 if vertical else len(matrix)-1
class Solution:
    def binary_search(self,matrix,target,start,vertical):
        lo = start
        hi = len(matrix[0])-1 if vertical else len(matrix)-1

        while hi >= lo:
            mid = (lo + hi)//2
            if vertical: # searching a column
                if matrix[start][mid] < target:
                    lo = mid + 1
                elif matrix[start][mid] > target:
                    hi = mid - 1
                else:
                    return True
            else: # searching a row
                if matrix[mid][start] < target:
                    lo = mid + 1
                elif matrix[mid][start] > target:
                    hi = mid - 1
                else:
                    return True
        
        return False

    def searchMatrix(self, matrix, target):
        # an empty matrix obviously does not contain `target`
        if not matrix:
            return False

        # iterate over matrix diagonals starting in bottom left.
        for i in range(min(len(matrix), len(matrix[0]))):
            vertical_found = self.binary_search(matrix, target, i, True)
            horizontal_found = self.binary_search(matrix, target, i, False)
            if vertical_found or horizontal_found:
                return True
        
        return False
```

# 5. 有序矩阵的 Kth Element

378\. Kth Smallest Element in a Sorted Matrix ((Medium))

[力扣](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

```html
matrix = [
  [ 1,  5,  9],
  [10, 11, 13],
  [12, 13, 15]
],
k = 8,

return 13.
```

```python  
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        q = []
        for mat in matrix:
            for i in mat:
                bisect.insort(q, i)
        return q[k - 1]
```

# 6. 一个数组元素在 [1, n] 之间，其中一个数被替换为另一个数，找出重复的数和丢失的数

645\. Set Mismatch (Easy)

[力扣](https://leetcode-cn.com/problems/set-mismatch/description/)

```html
Input: nums = [1,2,2,4]
Output: [2,3]
```
讲解：[Youtube]

```python

```

# 7. 找出数组中重复的数，数组值在 [1, n] 之间

287\. Find the Duplicate Number (Medium)

[力扣](https://leetcode-cn.com/problems/find-the-duplicate-number/description/)

要求不能修改数组，也不能使用额外的空间。

二分查找解法：

讲解：  
  

```python


```

# 8. 数组相邻差值的个数

667\. Beautiful Arrangement II (Medium)

[力扣](https://leetcode-cn.com/problems/beautiful-arrangement-ii/description/)

```html
给定两个整数 n 和 k，你需要实现一个数组，这个数组包含从 1 到 n 的 n 个不同整数，同时满足以下条件：
① 如果这个数组是 [a1, a2, a3, ... , an] ，那么数组 [|a1 - a2|, |a2 - a3|, |a3 - a4|, ... , |an-1 - an|] 中应该有且仅有 k 个不同整数；.
② 如果存在多种答案，你只需实现并返回其中任意一种.

数组元素为 1\~n 的整数，要求构建数组，使得相邻元素的差值不相同的个数为 k。
让前 k+1 个元素构建出 k 个不相同的差值，序列为：1 k+1 2 k 3 k-1 ... k/2 k/2+1.
```

讲解：[Youtube](https://www.youtube.com/watch?v=WLFXfcUVeeU)

```python
class Solution:
    def constructArray(self, n: int, k: int) -> List[int]:
        """
        :type n: int
        :type k: int
        :rtype: List[int]
        """
        res = list(range(1, n + 1))  # 刚开始有一个不同的差绝对值
        for i in range(1, k):  # 每翻转后面一次产生一个新的
            res[i:] = res[:i-1:-1]  # 翻转
        return res
```

# 9. 数组的度

697\. Degree of an Array (Easy)

[力扣](https://leetcode-cn.com/problems/degree-of-an-array/description/)

```html
Input: [1,2,2,3,1,4,2]
Output: 6
```

题目描述：数组的度定义为元素出现的最高频率，例如上面的数组度为 3。要求找到一个最小的子数组，这个子数组的度和原数组一样。

讲解：[Youtube](https://www.bilibili.com/video/BV1G4411S7hQ?from=search&seid=17197294950463230351)    

```python
class Solution(object):
    def findShortestSubArray(self, nums):
        left, right, count = {}, {}, {}
        for i, x in enumerate(nums):
            if x not in left: left[x] = i
            right[x] = i
            count[x] = count.get(x, 0) + 1

        ans = len(nums)
        degree = max(count.values())
        for x in count:
            if count[x] == degree:
                ans = min(ans, right[x] - left[x] + 1)

        return ans
```

# 10. 对角元素相等的矩阵

766\. Toeplitz Matrix (Easy)

[力扣](https://leetcode-cn.com/problems/toeplitz-matrix/description/)

```html
如果一个矩阵的每一方向由左上到右下的对角线上具有相同元素，那么这个矩阵是托普利茨矩阵。

给定一个 M x N 的矩阵，当且仅当它是托普利茨矩阵时返回 True。

示例 1:
输入: 
matrix = [
  [1,2,3,4],
  [5,1,2,3],
  [9,5,1,2]
]
输出: True
解释:
在上述矩阵中, 其对角线为:
"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]"。
各条对角线上的所有元素均相同, 因此答案是True。

示例 2:
输入:
matrix = [
  [1,2],
  [2,2]
]
输出: False
解释: 
对角线"[1, 2]"上的元素不同。

说明:
1.matrix 是一个包含整数的二维数组。
2.matrix 的行数和列数均在 [1, 20]范围内。
3.matrix[i][j] 包含的整数在 [0, 99]范围内。
进阶:
1.如果矩阵存储在磁盘上，并且磁盘内存是有限的，因此一次最多只能将一行矩阵加载到内存中，该怎么办？
2.如果矩阵太大以至于只能一次将部分行加载到内存中，该怎么办？
```

讲解：[Youtube](https://www.youtube.com/watch?v=YZVfCfZrDx8)    

```python
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        n=len(matrix)
        n1=len(matrix[0])
        for i in range(n-1):
            for j in range(n1-1):
                if matrix[i][j]!=matrix[i+1][j+1]:
                    return 0
        return 1
```

# 11. 嵌套数组

565\. Array Nesting (Medium)

[力扣](https://leetcode-cn.com/problems/array-nesting/description/)

```html
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation:
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```

题目描述：S[i] 表示一个集合，集合的第一个元素是 A[i]，第二个元素是 A[A[i]]，如此嵌套下去。求最大的 S[i]。

讲解：   

```python


```

# 12. 分隔数组

769\. Max Chunks To Make Sorted (Medium)

[力扣](https://leetcode-cn.com/problems/max-chunks-to-make-sorted/description/)

```html
Input: arr = [1,0,2,3,4]
Output: 4
Explanation:
We can split into two chunks, such as [1, 0], [2, 3, 4].
However, splitting into [1, 0], [2], [3], [4] is the highest number of chunks possible.
```

题目描述：分隔数组，使得对每部分排序后数组就为有序。

讲解：[Youtube](https://www.youtube.com/watch?v=twYLu4hEKnQ)    

```python
class Solution(object):
    def maxChunksToSorted(self, arr):
        ans = ma = 0
        for i, x in enumerate(arr):
            ma = max(ma, x)
            if ma == i: ans += 1
        return ans       
```
