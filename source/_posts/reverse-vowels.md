---
title: 反转字符串中的元音字母
date: 2020-10-16 16:33:01
categories:
- 技术

tags: 
    - 算法
    - 字符串
    - 反转
    - 双指针
---


## 题目描述
编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

<!-- more -->
## 示例
```
示例 1：
输入："hello"
输出："holle"

示例 2：
输入："leetcode"
输出："leotcede"
```

## 解法

### 关键信息
- 反转元音字母

### 思路
元音之母有： a, e, i, o, u, A, E, I, O, U

对于字符串反转问题，可使用双指针向中间移动，在移动过程中交换首尾指针的值来解决。

首尾指针，分别向中间移动，直至碰撞，在移动过程中
- 如果首尾指针所指的值都为元音，则交换
    - 否则如果首指针所指的元素，非元音，则首指针后移
    - 否则如果尾指针所指的元素，非元音，则尾指针迁移

### 代码
```go
func reverseVowels(s string) string {

	vowelMap := map[uint8]bool{
		byte('a'):true,
		byte('e'):true,
		byte('i'):true,
		byte('o'):true,
		byte('u'):true,
		byte('A'):true,
		byte('E'):true,
		byte('I'):true,
		byte('O'):true,
		byte('U'):true,
	}
	i, j := 0, len(s)-1
	temp:=[]byte(s)
	for i < j {
		a, b := temp[i], temp[j]
		if vowelMap[a] && vowelMap[b] {
			temp[i], temp[j] = b, a
			i++
			j--
		}
		if !vowelMap[a] {
			i++
		}
		if !vowelMap[b] {
			j--
		}
	}
	return string(temp)
}


func TestReverseVowels(t *testing.T) {
	assert.True(t, reverseVowels("hello") == "holle")
	assert.True(t, reverseVowels("aA") == "Aa")
	assert.True(t, reverseVowels("leetcode") == "leotcede")
}
```


