# 两数之和

## [题干](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 `nums` 和一个目标值 `target`, 请你在该数据组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

难度：简单（并不简单哇😂）

## 方法一：暴力法

思路很简单，双重循环就对了，时间复杂度是 `O(n^2)`，空间复杂度是 `O(1)`;

这种解法已经不能通过了，会报错 `超出时间限制`，代码实现如下：

python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]  
```

Emmmm...尴尬的是我只会 `暴力法`，昨晚花了一个小时，硬要用 `二分查找法` 解出来，然后被虐了😂，算法基础太薄弱了，除了冒泡和二分查找，其他啥也想不起来，今天一早就灰溜溜地来看官方解答了。

下面进入主题👇

## 方法二：两遍哈希表

思路大概是使用两次循环，时间复杂度是 `O(n)`，空间复杂度是 `O(n)`。

第一次循环，用一个哈希表存储数组中的元素及其对应的下标，在 `Python` 中用字典存储，`key` 对应数组元素，`value` 为相应的下标；

第二次循环，查找每个元素对应的目标元素 `target - nums[i]` 是否在表中，目标元素不能是 `nums[i]` 本身。代码实现如下：

python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_table = dict()
        for i in range(len(nums)):
            hash_table[nums[i]] = i
        for i in range(len(nums)):
            rest = target - nums[i]
            j = hash_table.get(rest)
            if j is not None and j != i:
                return [i, j]
```

## 方法三：一遍哈希表

在方法二的基础上，迭代的过程中，将元素插入哈希表，同时检查表中是否已经存在当前元素对应的目标元素。时间复杂度和空间复杂度等同于方法二。代码实现如下：

python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_map = dict()
        for index, elem in enumerate(nums):
            if hash_map.get(target - elem) is not None:
                return [index, hash_map.get(target - elem)]
            hash_map[elem] = index
```

这里有个地方需要注意⚠️，检查表中元素在前，元素插入表在后，否则，当出现 `target - num = num` 时，表中目标元素对应的索引将被替换成当前元素的索引。
