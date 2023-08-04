## leetcode-461-easy

[链接](https://leetcode.cn/problems/hamming-distance/description/)

##### 题目描述

两个整数之间的 [汉明距离](https://baike.baidu.com/item/汉明距离) 指的是这两个数字对应二进制位不同的位置的数目。

给你两个整数 `x` 和 `y`，计算并返回它们之间的汉明距离。

###### 示例一：

```
输入：x = 1, y = 4
输出：2
解释：
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
上面的箭头指出了对应二进制位不同的位置。
```

###### 相关知识点：

```
与：左右语句都为真时才为真 包括：逻辑与& 和短路与&&
或：左右有一则或超过一则语句为真时为真 包括：逻辑与| 和短路与||
非：取反，假时为真，真时为假 包括：逻辑非！
异或：左右相异时为真，左右相同时为假 包括：逻辑异或^
```

###### 思路：

利用异或计算对比每一位上的值

###### 代码：

```java
public int hammingDistance(int x, int y) {
	int ans = 0;
	for (int i = 0; i < 32; i++) {
		int a = (x >> i) & 1;
		int b = (y >> i) & 1;
		ans += a ^ b;
	}
	return ans;
}
```

###### 拓展：

**Brian Kernighan 算法**

Brian Kernighan算法可以用于清除二进制数中最右侧的1。Brian Kernighan算法的做法是先将当前数减一，然后在与当前数进行按位与运算。

我们可以使用Brian Kernighan算法进行优化，跳过两个1之间的0，直接对1进行计数。

###### 代码：

```java
public int hammingDistance(int x, int y) { 
	int s = x ^ y; 
	int ret = 0; 
	while( s != 0) { 
		s &= s - 1; 
		ret++;
	}
    return ret;
}
```

