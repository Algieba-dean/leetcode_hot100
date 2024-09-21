# 只出现一次的数字
```
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

```
 

**Example** 1:

**Input**: `nums = [2,2,1]`
**Output**: `1`

**Example** 2:

**Input**: `nums = [4,1,2,1,2]`
**Output**: `4`

**Example** 3:

**Input**: `nums = [1]`
**Output**: `1`
 

**Constraints**:

- `1 <= nums.length <= 3 * 104`
- `-3 * 104 <= nums[i] <= 3 * 104`
- `Each element in the array appears twice except for one element which appears only once.`

## 暴力解法
```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        if (nums.size() == 1) {
            return nums[0];
        }
        sort(nums.begin(), nums.end());
        if(nums[0]!=nums[1]){
            return nums[0];
        }
        for (auto i{1}; i < nums.size() - 1; ++i) {
            if (nums[i - 1] != nums[i] && nums[i] != nums[i + 1]) {
                return nums[i];
            }
        }
        return nums[nums.size() - 1];
    }
};
```
长度为3的滑动窗口，窗口中心从1到n-1，因为窗口点是窗口中心，需考虑两端的特殊情况, 此处左端单独讨论了，右端直接最终处理了.
### 评估
时间复杂度 O(nlog(n))

空间复杂度 O(1)

### 知识点

### 优化

## 对称加密
```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        auto result{0};
        for(const auto& num:nums){
            result^=num;
        }
        return result;
    }
};
```
位运算的异或重复两次后会将自己抵消掉，类似于对称加密.
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(1)**

### 知识点

### 优化