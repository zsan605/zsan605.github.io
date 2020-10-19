---
title: 合并两个有序数组
date: 2020-10-19 20:09:26
categories:
- 技术

tags: 
    - 算法
    - 数组
    - 合并
    - 双指针
---


## 题目描述
给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。

说明：

初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
 
<!-- more -->
## 示例
```
示例：
输入：
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出：[1,2,2,3,5,6]
 
提示：
-10^9 <= nums1[i], nums2[i] <= 10^9
nums1.length == m + n
nums2.length == n

```

## 解法

### 关键信息
- nums1,nums2为有序数组
- nums1空间为m+n
- 将nums2合并到nums1中，最终使nums1有序

### 思路
对于两个数组合并使用双指针碰撞解法

由于nums1和nums2有序，则可以选择从数组头开始合并，也可以选择从数组尾开始合并。但是，由于最终合并到nums1上，从头部合并，在合并过程中会导致数组向后的移动，所以选择从数组尾部开始合并。

具体合并思路如下：
1. 使用双指针i, j分别指向nums1,nums2的尾部
2. 开始从后往前遍历nums1,nums2，直至其中i==0或j==0
3. 判断nums1[i], nums2[j]的大小
4. 如果将nums2[j]较大,将其放在nums1[i+j-1]处，i--，跳转到2处
5. 否则将nums1[i]，放在nums1[i+j-1]处，j--，跳转到2处
6. 将nums2剩余数字，填充到nums1对应位置 

### 代码
```go
func merge(nums1 []int, m int, nums2 []int, n int) {

	for m > 0 && n > 0 {
		if nums1[m-1] > nums2[n-1] {
			nums1[m+n-1] = nums1[m-1]
			m--
		} else {
			nums1[m+n-1] = nums2[n-1]
			n--
		}
	}

	for n > 0 {
		nums1[n-1] = nums2[n-1]
		n--
	}

}

func TestMerge(t *testing.T) {
	nums1 := []int{1,2,3,0,0,0}
	nums2 := []int{2,5,6}
	merge(nums1, 3, nums2, 3)
	t.Log(nums1)
}

```



