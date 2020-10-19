---
title: 验证回文字符串 Ⅱ
date: 2020-10-19 13:09:41
categories:
- 技术

tags: 
    - 算法
    - 字符串
    - 回文
    - 双指针
---


## 题目描述

给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。

<!-- more -->
## 示例
```
示例 1
输入: "aba"
输出: True

示例 2
输入: "abca"
输出: True
解释: 你可以删除c字符。

注意:
字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。
```

## 解法

### 关键信息
- 非空字符串
- 删除0个或1个字符后为回文字符串

### 思路
判断一个字符串是否为回文字符串，可以使用双指针碰撞解法。

对本题来说，存在三种情况：
1. 字符串为回文字符串，删除0个字符
2. 字符串不为回文字符串，删除1个字符后，为回文字符串
3. 字符串不为回文字符串，删除1个字符后，不为回文字符串

对于字符串 s 使用双指针 i，j 分别指向字符串首尾，在遍历过程中，如果i,j所对应的字符不相等，则出现第二，三种情况。

此时只需判断s[i+1,j] 和s[i,j-1]是否为回文字符串，如果存在一个为回文则属于第二种情况，否则为第三种情况。

### 代码
```go
func validPalindrome(s string) bool {

	i, j, isPalindrome := validPalindromeFunc(s)
	if isPalindrome {
		return true
	}

	_, _, isPalindrome = validPalindromeFunc(s[i+1:j+1])
	if isPalindrome {
		return true
	}

	_, _, isPalindrome = validPalindromeFunc(s[i:j])
	if isPalindrome {
		return true
	}

	return false
}

func validPalindromeFunc(temp string) (int, int, bool) {
	i, j := 0, len(temp) -1
	for i < j {
		if temp[i] != temp[j] {
			return i, j, false
		}
		i++
		j--
	}
	return i, j, true
}

func TestValidPalindrome(t *testing.T) {
	assert.True(t, validPalindrome("abcddba"))
}

```


