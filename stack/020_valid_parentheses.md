# 有效的括号
```
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
```
 

**Example** 1:

**Input**: `s = "()"`

**Output**: `true`

**Example** 2:

**Input**:  `s = "()[]{}"`

**Output**: `true`

**Example** 3:

**Input**: `s = "(]"`

**Output**: `false`

**Example** 4:

**Input**: `s = "([])"`

**Output**: `true`

 

**Constraints**:

- `1 <= s.length <= 104`
- `s consists of parentheses only '()[]{}'.`

## 栈
```C++
class Solution {
public:
    bool isValid(string s) {
        stack<char> parentheses;
        if (s.size() % 2 != 0) {
            return false;
        }
        auto dummy{'-'};
        parentheses.emplace(dummy);
        for (const auto& c : s) {
            if (c == '(' || c == '[' || c == '{') {
                parentheses.emplace(c);
            } else if ((c == ')') && (parentheses.top() == '(')) {
                parentheses.pop();
            } else if ((c == ']') && (parentheses.top() == '[')) {
                parentheses.pop();
            } else if ((c == '}') && (parentheses.top() == '{')) {
                parentheses.pop();
            } else {
                return false;
            }
        }
        if (parentheses.top() == dummy) {
            return true;
        }
        return false;
    }
};
```
加入的时候匹配即消，无匹配直接false，终了空则true.
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(n)**

### 知识点
- for each loop的使用
- `std::string`的size是除开\0的
- `std::stack`有push(e), pop(), top(),empty(), 若top为空时调用top(),会抛异常
- `std::stack`支持emplace()

- 若只有奇数个元素，则必不匹配

### 优化
