---
title: 两数之和 II - 输入有序数组
date: 2020-10-15 17:00:12
categories:
- 技术

tags: 
    - 算法
    - 数组
    - 查找

---


## 题目描述
给定一个已按照升序排列的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

说明:

返回的下标值（index1 和 index2）不是从零开始的。

你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

<!-- more -->
## 示例
```
输入:
numbers = [2, 7, 11, 15], target = 9

输出:
[1,2]

解释: 
2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

## 解法

### 关键信息
- 数组有序且升序
- 数组下标从1开始计数

### 思路
数组内两数之和，使用双指针来遍历。

由于数组是升序，则可将指针分别放于数组两端。然后向中间遍历，如果两数之和小于目标值，左侧指针前移；如果两数之和大于目标值，右侧指针后移；直至两指针相遇。

### 代码
```go
func twoSum(numbers []int, target int) []int {

	if len(numbers) < 2 {
		return nil
	}

	i, j := 0, len(numbers)-1
	for i < j {
		if numbers[i]+numbers[j] == target {
			return []int{i, j}
		} else if numbers[i]+numbers[j] > target {
			j--
		} else {
			i++
		}
	}
	return nil
}

func TestTwoSum(t *testing.T) {
	nums := []int{2,7,11,15}
	assert.True(t, twoSum(nums, target) == 9)
}
```


