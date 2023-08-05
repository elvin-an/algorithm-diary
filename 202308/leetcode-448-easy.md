## leetcode-448-easy

[找到所有数组中消失的数字](https://leetcode.cn/problems/find-all-numbers-disappeared-in-an-array/description/)

##### 题目描述

给你一个含n个整数的数组nums，其中nums[i]在区间[1,n]内，请找出所有在[1, n]范围内但没有出现在nums中的数字，并以数组的形式返回结果。

###### 示例1：
```
    输入：nums = [4,3,2,7,8,2,3,1]
    输出：[5,6]
```

###### 思路1：

初始化一个大小为n，且每个元素的值为-1的数组，遍历nums，并将nums[i] - 1对应小标的值更新为1，统计值为-1的下标
```
	public List<Integer> findDisappearedNumbers(int[] nums) {
		List<Integer> ans = new ArrayList<>();
		List<Integer> showed = new ArrayList<>(nums.length);
		for (int i = 0; i < nums.length; i++) {
			showed.add(-1);
		}
		for (int num : nums) {
			showed.set(num - 1, 1);
		}
		for (int i = 0; i < nums.length; i++) {
			if (showed.get(i) == -1) {
				ans.add(i + 1);
			}
		}
		return ans;
	}
```

**问题：**
使用了额外的数组记录数据是否出现过，增加了空间复杂度

###### 思路2：

原地修改，遍历nums,每遇到一个数x，就让nums[x - 1]增加n,最后遍历nums判断nums[i]是否大于n
```
    public List<Integer> findDisappearedNumbers(int[] nums) {
        int n = nums.length;
        for (int num : nums) {
            int x = (num - 1) % n;
            nums[x] += n;
        }
        List<Integer> ans = new ArrayList<>();
        for (int i = 0; i < n ; i ++) {
            if (nums[i] < n) {
                ans.add(i + 1);
            }
        }
        return ans;
	}
```
