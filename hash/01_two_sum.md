# 两数之和
```
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.
```

 

**Example** 1:

**Input**: `nums = [2,7,11,15], target = 9`
**Output**: `[0,1]`
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

**Example** 2:

**Input**: `nums = [3,2,4], target = 6`
**Output**: `[1,2]`

**Example** 3:

**Input**: `nums = [3,3], target = 6`
**Output**: `[0,1]`
 

**Constraints**:

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- `Only one valid answer exists.`
 

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

## 暴力法
最直接的解法,通过两层循环扫描
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (auto i{0};i<nums.size();i++){
            for (auto j{i+1}; j<nums.size(); j++){
                if (nums[i] + nums[j]!= target){
                    continue;
                }
                return {i,j};
            }
        }
    return {};
    }
};
```
### 评估
时间复杂度：O(n^2)

空间复杂度 O(1)

### 知识点
- 常年写for-each忘记for循环写法 `for(auto i{0};i<len;i++)`

- 第二层的循环可以从`i+1`开始,也不用担心循环会越界，有循环条件限制， 且因为是正向扫描，在左边不会出现任何结果，所以可以直接跳过.
- 提前判断跳出条件，减少循环嵌套层数.


### 优化方案
暂无

## 哈希表
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        if(nums.size() == 0 || nums.size() == 1){
            return {};
        }
        unordered_map<int,vector<int>> num2pos;
        for(auto i(0); i < nums.size();i++){
            num2pos[nums[i]].emplace_back(i);
        }
        for(auto i(0); i < nums.size();i++){
            const auto& posVec{num2pos[target-nums[i]]};
            if(posVec.size()==0){
                continue;
            }
            for(const auto& pos: posVec){
                if(pos == i){
                    continue;
                }
                return {i,pos};
            }
        }
        return {};
    }
};
```

### 评估
时间复杂度 O(2n)

空间复杂度 O(n)

### 知识点
- 返回值优化，即在返回值时候进行{}列表初始化作为返回值，是`C++11`的特性
- undordered_map用**operator[]**取值，若无该key，会默认初始一个. 用**at**取值，若无key会直接**抛异常**
- vector的emplace_back会减少额外复制或移动, 减少临时对象产生.

- 注意这里不能直接`unordered_map<int, int>`， 因为会出现 target=6, 两个值为3这种情况，key有唯一性.

### 优化方案
- hash表的部分，用vector只是单纯解决重复值问题，可以单拎出来讨论，如果是重复值，必定是对半开的，能提前预判处理，找到第二个值的时候，立马就可以返回
- 更进一步，完全可以在一次循环中处理完，类似于备忘录，往里面放值的时候，就一边查哈希表中是否有另一个值，如果有，因为只是两数和，必定拆为两个数，不会有两数以上相同，直接返回当前序号和表中值即可。
- 如果再n数之和，或者要考虑单独一个数满足的情况，就可以组一个vector了
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        if(nums.size() == 0 || nums.size() == 1){
            return {};
        }
        unordered_map<int,int> num2pos;
        for (auto i{0}; i < nums.size(); ++i){
            const auto& it{num2pos.find(target-nums[i])};
            if (it != num2pos.end()){
                return {i, it->second};
            }
            num2pos[nums[i]] = i;
        }
        return {};
    }
};
```
优化后
时间复杂度 O(n)
空间复杂度 O(n)