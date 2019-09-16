# 删除排序数组中的重复项

### [题干](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

给定一个排序数组，你需要在[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

难度：简单

乍一看，输出是新数组的长度，一想，将数组转换成集合，然后输出集合的长度，不就搞定了嘛。然后马上去提交，结果 `解答错误`，输出的是一个数组！

原来我忽略了要在原数组上做修改，使用 `O(1)` 额外空间完成😅，下面进入正题吧。

### 我的解法：哈希表

受到 [两数之和](https://leetcode-cn.com/problems/two-sum/) 的影响，我用字典的方式解了该题😓，顺便还用到了 `Python` 的深拷贝。执行时间 804ms......

时间复杂度和空间复杂度均为 `O(n)`, 代码实现如下：

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        hash_map = dict()
        nums_cp = copy.deepcopy(nums)
        for index, elem in enumerate(nums_cp):
            if elem in hash_map:
                nums.remove(elem)
            else:
                hash_map[elem] = index
        return len(nums)
```

注意⚠️：虽然这种解法通过了，但是它同样忽略了题干 - 空间复杂度要求为 `O(1)` (在审题方面，我装瞎能力很强呢 ◔ ‸◔？)

### 官方解法：双指针法

我的解法中忽略了一个很重要的信息：数组是有序的！

官方解法中提到了双指针，思路是用两个指针 i(慢指针), j(快指针)。时间复杂度：`O(n)`, 空间复杂度：`O(1)`.

只要 `nums[i] == nums[j]`, j 加1，跳过重复项；当遇到 `nums[i] != nums[j]`, i 递增，然后把 nums[j] 值复制给 nums[i].

Show me codeヽ(✿ﾟ▽ﾟ)ノ

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0

        i = 0
        for j in range(1, len(nums)):
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]
        return i + 1
```
