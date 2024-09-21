# 移动零
```
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.
```

 

**Example** 1:

**Input**: `nums = [0,1,0,3,12]`
**Output**: `[1,3,12,0,0]`

**Example** 2:

**Input**: `nums = [0]`
**Output**: `[0]`
 

**Constraints**:

- `1 <= nums.length <= 104`
- `-231 <= nums[i] <= 231 - 1`
 

Follow up: Could you minimize the total number of operations done?

## 暴力解法
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        vector<int> retVec(nums.size(), 0);
        auto i{0};
        for (const auto& num:nums){
            if(num!=0){
                retVec[i]=num;
                ++i;
            }
        }
        nums=retVec;
    }
};
```
### 评估
时间复杂度 O(n)

空间复杂度 O(n)

PS: 需要额外空间开辟

### 知识点
- 初始化vector为10个0， vector<int>(10,0);

## 就地处理
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        auto left{0};
        auto right{0};
        while (left < nums.size()) {
            if (nums[left] != 0) {
                ++left;
                ++right;
                continue;
            }
            ++right;
            while (right < nums.size() && nums[right] == 0) {
                ++right;
            }
            if (right == nums.size()){
                return;
            }
            nums[left] = nums[right];
            nums[right] = 0;
            ++left;
            right = left;
        }
    }
};
```
由于其本质就是，将左边的每一个0和右边第一个非0数交换，故有一个左指针先找到第一个0， 然后从左指针右边开始扫描找到第一个非0数进行交换，再继续移动左指针。

### 优化版
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        const auto n{nums.size()};
        auto left{0};
        auto right{0};
        while (right < n) {
            if (nums[right]) {
                swap(nums[left], nums[right]);
                left++;
            }
            right++;
        }
    }
};
```
想象处理好的数据，分为两部分，左边为非0数，右边为0
### 评估
时间复杂度 O(n)
空间复杂度 O(1)

### 知识点
无