---
title: 矩阵中的查找
date: 2020-10-14 11:57:52
categories:
- 开发
tags: 
    - 算法
    - 矩阵
    - 查找
---

## 题目描述
给定一个二维数组，其每一行从左到右递增排序，从上到下也是递增排序。给定一个数，判断这个数是否在该二维数组中。

<!-- more -->
## 输入
```
matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

target 如下：
target = 5
target = 20
```

## 输出
```
target = 5, return true.
target = 20, return false.
```
## 要求
时间复杂度 O(M+N)，空间复杂度 O(1)


## 解法

### 关键信息
- 矩阵行内从左到右递增
- 矩阵列内从上到下递增

### 思路
分析可得，矩阵中的一个数的左边的数都小于它，下方的数都大于它。

因此可在矩阵上找一个数与目标进行比较，如果大于目标值，则取左边的的值继续比较；如果小于目标值，则取下边的值继续比较；如果相等，则返回true

为了能够遍历的整个矩阵，选取的数应为矩阵左上角。

同理也可以选择右下角，此时，如果大于目标值，则取上边的的值继续比较；如果小于目标值，则取右边的值继续比较；如果相等，则返回true

### 代码
```go
func findNumberFromMatrix(target int, matrix [][]int) bool {
	if len(matrix) == 0 || len(matrix[0]) == 0 {
		return false
	}

	row, col := 0, len(matrix[0])-1
	for row < len(matrix) && col >= 0 {
		if target == matrix[row][col] {
			return true
		} else if target < matrix[row][col] {
			col--
		} else {
			row++
		}
	}

	return false
}


func TestFindNumberFromMatrix(t *testing.T) {
	matrix := [][]int{
		{1, 4, 7, 11, 15},
		{2, 5, 8, 12, 19},
		{3, 6, 9, 16, 22},
		{10, 13, 14, 17, 24},
		{18, 21, 23, 26, 30},
	}

	assert.True(t, findNumberFromMatrix(12, matrix))
	assert.False(t, findNumberFromMatrix(20, matrix))
	assert.False(t, findNumberFromMatrix(0, matrix))
}

```


