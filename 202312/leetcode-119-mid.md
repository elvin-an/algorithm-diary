## leetcode-119-mid

[最长连续序列](https://leetcode.cn/problems/WhsWhI/description/)

##### 题目描述
给定一个未排序的整数数组 nums ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

###### 示例1
```
    输入：nums = [100,4,200,1,3,2]
    输出：4
    解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。
```

###### 示例2
```
    输入：nums = [0,3,7,2,5,8,4,6,0,1]
    输出：9
```

###### 思路1
暴力：从头开始遍历判断x+1是否在数组中

```
    def longestConsecutive1(nums: List[int]) -> int:
        longest_streak = 0
        for num in nums:
            current_streak = 1
            current_num = num
            while current_num + 1 in nums:
                current_num += 1
                current_streak += 1
            longest_streak = max(current_streak, longest_streak)
        return longest_streak
```

###### 思路2
因为暴力求解都会从x+1,x+2,x+3计算，优化点如果x-1在数组中，那么x可以交给x-1来计算

```
    def longestConsecutive(nums: List[int]) -> int:
        longest_streak = 0

        # 去重
        num_set = set(nums)
            for num in num_set:
                # 避免重复计算 因为如果num - 1在num_set在num_set中，num会从num-1计算
                if num - 1 not in num_set:
                    current_num = num
                    current_streak = 1

                    while current_num + 1 in num_set:
                        current_num += 1
                        current_streak += 1
                    longest_streak = max(longest_streak, current_streak)

        return longest_streak
```


