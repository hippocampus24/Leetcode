<!-- GFM-TOC -->
* [1. 有序数组的 Two Sum](#1-有序数组的-two-sum)
* [2. 两数平方和](#2-两数平方和)
* [3. 反转字符串中的元音字符](#3-反转字符串中的元音字符)
* [4. 回文字符串](#4-回文字符串)
* [5. 归并两个有序数组](#5-归并两个有序数组)
* [6. 判断链表是否存在环](#6-判断链表是否存在环)
* [7. 最长子序列](#7-最长子序列)
<!-- GFM-TOC -->


双指针主要用于遍历数组，两个指针指向不同的元素，从而协同完成任务。

# 1. 有序数组的 Two Sum

167\. Two Sum II - Input array is sorted (Easy)

[力扣](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/description/)

```html
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

题目描述：在有序数组中找出两个数，使它们的和为 target。

使用双指针，一个指针指向值较小的元素，一个指针指向值较大的元素。指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。

- 如果两个指针指向元素的和 sum == target，那么得到要求的结果；
- 如果 sum > target，移动较大的元素，使 sum 变小一些；
- 如果 sum < target，移动较小的元素，使 sum 变大一些。

数组中的元素最多遍历一次，时间复杂度为 O(N)。只使用了两个额外变量，空间复杂度为  O(1)。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/437cb54c-5970-4ba9-b2ef-2541f7d6c81e.gif" width="200px"> </div><br>

```python
class Solution:
    def twoSum(self,numbers:List[int],target:int) -> List[int]:
        if not numbers : return [0,0]
        i, j = 0, len(numbers) - 1
        while i < j:
            s = numbers[i] + numbers[j]
            if s == target:
                return [i+1, j+1]
            elif s < target:
                i += 1
            else:
                j -= 1
        return [0,0]
```

# 2. 两数平方和

633\. Sum of Square Numbers (Easy)

[力扣](https://leetcode-cn.com/problems/sum-of-square-numbers/description/)

```html
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```

题目描述：判断一个非负整数是否为两个整数的平方和。

给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c。

示例1:

输入: 5
输出: True
解释: 1 * 1 + 2 * 2 = 5
 

示例2:

输入: 3
输出: False

```python
class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        i,j=0,int(c**0.5)
        while i <=j:
            if i*i + j*j == c:
                return True
            elif i*i + j*j > c:
                j-=1
            elif i*i + j*j<c:
                i+=1
        return False
```

# 3. 反转字符串中的元音字符

345\. Reverse Vowels of a String (Easy)

[力扣](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/description/)

```html
Given s = "leetcode", return "leotcede".
```

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/a7cb8423-895d-4975-8ef8-662a0029c772.png" width="400px"> </div><br>

使用双指针，一个指针从头向尾遍历，一个指针从尾到头遍历，当两个指针都遍历到元音字符时，交换这两个元音字符。

为了快速判断一个字符是不是元音字符，我们将全部元音字符添加到集合 HashSet 中，从而以 O(1) 的时间复杂度进行该操作。

- 时间复杂度为 O(N)：只需要遍历所有元素一次
- 空间复杂度 O(1)：只需要使用两个额外变量

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/ef25ff7c-0f63-420d-8b30-eafbeea35d11.gif" width="400px"> </div><br>

```python
class Solution(object):
    def reverseVowels(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = list(s)         #转换为列表
        cs = {'A','E','I','O','U','a','e','i','o','u'}      #元音哈希表
        l = 0           #左指针
        r = len(s)-1    #右指针

        while l<r:
            if s[l] in cs and s[r] in cs:    #都是原音则互换，移动两边指针
                temp = s[r]
                s[r] = s[l]
                s[l] = temp
                r = r-1
                l = l+1
            elif s[l] in cs and s[r] not in cs:  #有一个不是元音则移动一边指针
                r = r-1
            elif s[l] not in cs and s[r] in cs:  #有一个不是元音则移动一边指针
                l = l+1
            else:                               #都不是原音则互换，移动两边指针
                l = l+1
                r = r-1
        return ''.join(s)                      #将列表转换为字符串
    
```

# 4. 回文字符串

680\. Valid Palindrome II (Easy)

[力扣](https://leetcode-cn.com/problems/valid-palindrome-ii/description/)

```html
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

题目描述：可以删除一个字符，判断是否能构成回文字符串。

所谓的回文字符串，是指具有左右对称特点的字符串，例如 "abcba" 就是一个回文字符串。

使用双指针可以很容易判断一个字符串是否是回文字符串：令一个指针从左到右遍历，一个指针从右到左遍历，这两个指针同时移动一个位置，每次都判断两个指针指向的字符是否相同，如果都相同，字符串才是具有左右对称性质的回文字符串。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/fcc941ec-134b-4dcd-bc86-1702fd305300.gif" width="250px"> </div><br>

本题的关键是处理删除一个字符。在使用双指针遍历字符串时，如果出现两个指针指向的字符不相等的情况，我们就试着删除一个字符，再判断删除完之后的字符串是否是回文字符串。

在判断是否为回文字符串时，我们不需要判断整个字符串，因为左指针左边和右指针右边的字符之前已经判断过具有对称性质，所以只需要判断中间的子字符串即可。

在试着删除字符时，我们既可以删除左指针指向的字符，也可以删除右指针指向的字符。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/db5f30a7-8bfa-4ecc-ab5d-747c77818964.gif" width="300px"> </div><br>

```python
class Solution(object):
    def validPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        isPalindrome = lambda s: s == s[::-1]
        strPart = lambda s, x: s[:x] + s[x + 1:]
        left = 0
        right = len(s) - 1
        while left < right:
            if s[left] != s[right]:
                return isPalindrome(strPart(s, left)) or isPalindrome(strPart(s, right))
            left += 1
            right -= 1
        return True
```

# 5. 归并两个有序数组

88\. Merge Sorted Array (Easy)
[力扣](https://leetcode-cn.com/problems/merge-sorted-array/description/)

```html
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

题目描述：把归并结果存到第一个数组上。

需要从尾开始遍历，否则在 nums1 上归并得到的值会覆盖还未进行归并比较的值。

设a为位置变量。
本题难点在于边界处理：
(1)m=0和n=0的情况要独立讨论；
(2)确定nums1的元素是否都进行过对比。

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        if m == 0:
            nums1[:] = nums2[:]
        elif n == 0:
            nums1 = nums1
        else:
            a = 0
            while len(nums2) > 0:
                if nums1[a] <= nums2[0]: 
                    if a < m+n-len(nums2):
                        a += 1
                    else:
                        nums1[m+n-len(nums2):] = nums2[:]
                        break                    
                else:
                    n2 = nums2.pop(0)
                    nums1[a+1:m+n] = nums1[a:m+n-1]
                    nums1[a] = n2   
```

# 6. 判断链表是否存在环

141\. Linked List Cycle (Easy)

[力扣](https://leetcode-cn.com/problems/linked-list-cycle/description/)

使用双指针，一个指针每次移动一个节点，一个指针每次移动两个节点，如果存在环，那么这两个指针一定会相遇。
理解：
思路：定义一个快指针和慢指针,每次快指针走2步，慢指针走1步，判断快指针是否与慢指针重逢
时间复杂度O(n+k)：
情况一：链表部分成环O(n)；
部分成环时，快指针先于慢指针进入环，慢指针进环时间O(n)；当快慢指针都进入环，假设环节点数量为K,当快慢指针第一次相遇时，快指针至少已经在环内已经比慢指针多走一圈(多走的这一圈是当慢指针进入后开始算的)，时间O(k)； 综上，时间复杂度O(k+n)，即为O(n)

```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        slow = fast = head
        # if not head：  # 没必要这样写可以加入while循环判断更简洁
        #     return False

        while fast and fast.next:  # 防止head为空和出现空指针的next的情况
            slow = slow.next
            fast = fast.next.next
            if slow is fast:
                return True

        return False
```

# 7. 最长子序列

524\. Longest Word in Dictionary through Deleting (Medium)

[力扣](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/description/)

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output:
"apple"
```

题目描述：删除 s 中的一些字符，使得它构成字符串列表 d 中的一个字符串，找出能构成的最长字符串。如果有多个相同长度的结果，返回字典序的最小字符串。

通过删除字符串 s 中的一个字符能得到字符串 t，可以认为 t 是 s 的子序列，我们可以使用双指针来判断一个字符串是否为另一个字符串的子序列。

```python

```

