---
title: 数字中的重复数字
date: 2020-10-13 17:47:17
categories:
- 技术

tags: 
    - 算法
    - 数组
    - 重复数组

---

## 题目描述
在一个长度为 n 的数组里的所有数字都在 0 到 n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字是重复的，也不知道每个数字重复几次。请找出数组中任意一个重复的数字。

<!-- more -->
## 输入
```
{2, 3, 1, 0, 2, 5}
```

## 输出
```
2
```
## 要求
时间复杂度 O(N)，空间复杂度 O(1)


## 解法

### 关键信息
- 数组长度为 n
- 数组元素范围 0到n-1

### 思路
对于 [0, n-1] 范围的数组，可以将值为 i 的元素调整到第 i 个位置上求解。

由于本题查找重复数字，则在调整过程中，如果i位置已经为i的话，则证明i为重复数字。

### 代码
```go
func repeatNumberInArray(arr []int) int {

    if len(arr) <= 1 {
		return -1
	}

	for i, _ := range arr {
		for arr[i] != i {
			if arr[i] == arr[arr[i]] {
				return arr[i]
			}

			arr[i], arr[arr[i]] = arr[arr[i]], arr[i]
		}
	}
	return -1
}


func TestRepeatNumberInArray(t *testing.T) {
	arr := []int{2, 3, 1, 0, 2, 5}
	arr1 := []int{3, 1, 0, 2, 2, 5}
	arr2 := []int{3, 1, 0, 2, 4}
	assert.True(t, repeatNumberInArray(arr) == 2)
	assert.True(t, repeatNumberInArray(arr1) == 2)
	assert.True(t, repeatNumberInArray(arr2) == -1)
}

```


