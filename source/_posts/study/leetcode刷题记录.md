---
title: leetcode刷题记录
date: 2023-07-18 21:51:41
sticky: true
tags: 
    - 刷题
categories:
    - [学习]
---

## 两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

示例 1：

```shell
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

示例 2：

```shell
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

示例 3：

```shell
输入：nums = [3,3], target = 6
输出：[0,1]
```
<!-- more -->

* 解法一：暴力求解

```Python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    l = len(nums)
    for i in range(l):
        for j in range(i+1, l):
            if nums[i] + nums[j] == target:
                return int[]{i, j}
    return []
```

* 解法二：哈希表映射求解

> 通过查找target-num的值是否存在hashTable中
> 如果不存在，则存入key-value --> num-i
> 如果存在，则去除target-num值的i值，与当前的i值

```Python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    hashTable = dict()
    for i, num in enumerate(nums):
        if target - num in hashTable:
            return [hashTable[target - num], i]
        hashTable[num[i]] = i
    return []

```
