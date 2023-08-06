## leetcode-438-mid

[找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/description/)

##### 题目描述

给定两个字符串 s 和 p，找到 s 中所有 p 的 **异位词** 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。
**异位词** 指由相同字母重排列形成的字符串（包括相同的字符串）。

###### 示例1：
```
    输入: s = "cbaebabacd", p = "abc"
    输出: [0,6]
    解释:
    起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
    起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
```

###### 示例2：
```
    输入: s = "abab", p = "ab"
    输出: [0,1,2]
    解释:
    起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
    起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
    起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
```

###### 思路：
对s滑动窗口，统计子串中字符的个数是否与p中相等

###### 代码：

```
public List<Integer> findAnagrams2(String s, String p) {
    int sLen = s.length(), pLen = p.length();
    if (sLen < pLen) {
        return new ArrayList<>();
    }
    List<Integer> ans = new ArrayList<>();
    int[] sCount = new int[32];
    int[] pCount = new int[32];
    // 初始化p中字符出现的次数
    for (int i = 0; i < pLen; i++) {
        ++sCount[s.charAt(i) - 'a'];
        ++pCount[p.charAt(i) - 'a'];
    }
    if (Arrays.equals(sCount, pCount)) {
        ans.add(0);
    }

    // 开始滑动窗口
    for (int i = 0; i < sLen - pLen; i++) {
        --sCount[s.charAt(i) - 'a'];
        ++sCount[s.charAt(i + pLen) - 'a'];
        if (Arrays.equals(sCount, pCount)){
            ans.add(i + 1);
        }
    }
    return ans;
}
```
