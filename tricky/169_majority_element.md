# 多数元素
```
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.
```
 

**Example 1**:

**Input**: `nums = [3,2,3]`
**Output**: `3`

**Example 2**:

**Input**: `nums = [2,2,1,1,1,2,2]`
**Output**: `2`
 

**Constraints**:

- `n == nums.length`
- `1 <= n <= 5 * 104`
- `-109 <= nums[i] <= 109`
 

**Follow-up**: Could you solve the problem in linear time and in `O(1)` space?

## 暴力解法
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[(nums.size()-1)/2];
    }
};
```
直接排序看中间的数字
### 评估
时间复杂度 **O(nlog(n))**

空间复杂度 **O(1)**

### 知识点

### 优化
题解要求`时间复杂度O(n)`且`空间复杂度O(1)`


## 缩圈法
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        stack<int> scope;
        for(const auto&num: nums){
            if(scope.empty()||scope.top()==num){
                scope.emplace(num);
            }else{
                scope.pop();
            }
        }
        return scope.top();
    }
};
```
因为众数是过半了的，任意删去两个不同的数，众数没有变化。 考虑边界情况, (n/2)+1数为p，其余为q ,任意删除2个不同数 最差的情况n的占比从 ((n/2)+1)/n到((n/2))/(n-2)，仍过半.到最后会变成全同.即找到了众数.

想象每个数字代表一个阵营, 进来的阵营不同俩人就相互厮杀，互相抵消，由于众数阵营占比过半，最终剩下的必然是众数阵营.
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(n)**

### 知识点

### 优化
目前的空间复杂度为O(n)仍需要优化. 将栈变为用指针遍历，只用维护一个当前剩下的阵营和人数即可。

```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        auto remainNum{nums[0]};
        auto remainsCount{1};
        for(auto i{1}; i<nums.size();++i){
            if(remainsCount==0){
                remainNum = nums[i];
                ++remainsCount;
                continue;
            }
            if(nums[i]==remainNum){
                ++remainsCount;
            }else{
                --remainsCount;
            }
        }
        return remainNum;
    }
};
```
时间复杂度 **O(n)**

空间复杂度 **O(1)**