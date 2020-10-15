---
title: 平方之和
date: 2020-10-15 18:04:22
categories:
- 技术

tags: 
    - 算法
    - 查找
    - 双指针

---
## 题目描述
给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a\*a + b\*b = c 。

<!-- more -->
## 示例
```
输入：c = 5
输出：true
解释：1 * 1 + 2 * 2 = 5

输入：c = 3
输出：false

输入：c = 4
输出：true

输入：c = 2
输出：true

输入：c = 1
输出：true
```
## 提示
```
0 <= c <= 231 - 1
```
## 解法

### 关键信息
- 整数c非负
- a\*a + b\*b = c

### 思路

根据题目信息有以下理解：
- 由于负正数的平方和正整数的平方一样，故不考虑负数
- 可以理解为在0~n的数组之间取一两个数a,b，使得a\*a+b\*b = c

这样解法就类似 [两数之和 II - 输入有序数组](https://zsan605.github.io/2020/10/15/two-sum/) 

由于c可以由 0\*0 + b\*b 计算获得。则a,b的最小值为0, 最大值为 c 的 平方根向下取整得max。

然后使用双指针来遍历,a从0开始递增，b从max开始递减，直至相遇，遍历过程如下

- 如果a\*a+b\*b大于c, b递减
- 如果a\*a+b\*b小于c, a递增

### 代码
```go

func judgeSquareSum(c int) bool {

	a, b := 0, int(math.Sqrt(float64(c)))

	target := 0
	for a <= b {
		target = a*a + b*b
		if c == target {
			return true
		} else if target > c {
			j--
		} else {
			i++
		}
	}
	return false
}


func TestJudgeSquareSum(t *testing.T) {
	assert.True(t, judgeSquareSum(5))
	assert.True(t, judgeSquareSum(4))
	assert.False(t, judgeSquareSum(3))
	assert.True(t, judgeSquareSum(2))
	assert.True(t, judgeSquareSum(1))
	assert.False(t, judgeSquareSum(2147482647))
}
```


