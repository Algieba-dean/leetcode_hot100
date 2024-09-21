# 搜索插入位置
```Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.
```

 

**Example** 1:


**Input**: `nums = [1,3,5,6], target = 5`
**Output**: `2`

**Example** 2:

**Input**: `nums = [1,3,5,6], target = 2`
**Output**: `1`

**Example** 3:

**Input**: `nums = [1,3,5,6], target = 7`
**Output**: `4`
 

**Constraints**:

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums contains distinct values sorted in ascending order.`
- `-104 <= target <= 104`

## 暴力解法
```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        if (target <= nums[0]) {
            return 0;
        }
        for (auto i{0}; i < nums.size() - 1; ++i) {
            if (nums[i] < target && target <= nums[i + 1]) {
                return i + 1;
            }
        }
        return nums.size();
    }
};
```
挨着找，找到前面小于，后面大于等于即插入。注意首尾
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(1)**

### 知识点

### 优化


## 二分搜索法
```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        auto left{0};
        auto right{nums.size() - 1};
        auto mid{(left + right + 1) / 2};

        while (right - left > 1) {
            if (target < nums[mid]) {
                right = mid;
            } else {
                left = mid;
            }
            mid = (left + right + 1) / 2;
        }
        if (target <= nums[left]) {
            return left;
        }
        if (target <= nums[right]) {
            return right;
        }
        return right + 1;
    }
};
```
二分搜索, 注意循环终止条件, 注意最终输出值
### 评估
时间复杂度 **O(log(n))**

空间复杂度 **O(1)**

### 知识点

### 优化