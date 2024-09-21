# 环形链表
```
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.
```

 

**Example** 1:

![alt text](../images/image-8.png)

**Input**: `head = [3,2,0,-4], pos = 1`
**Output**: `true`

Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

**Example** 2:

![alt text](../images/image-9.png)

**Input**: `head = [1,2], pos = 0`
**Output**: `true`

Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

**Example** 3:

![alt text](../images/image-10.png)

**Input**: `head = [1], pos = -1`
**Output**: `false`

Explanation: There is no cycle in the linked list.
 

**Constraints**:

- `The number of the nodes in the list is in the range [0, 104].`
- `-105 <= Node.val <= 105`
- `pos is -1 or a valid index in the linked-list.`
 

Follow up: Can you solve it using O(1) (i.e. constant) memory?
## 暴力解法
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_set<ListNode*> shownNodes;
        while(head!=nullptr){
            if(shownNodes.count(head)>0){
                return true;
            }
            shownNodes.emplace(head);
            head = head->next;
        }
        return false;
    }
};
```

直接判断是否有出现过的节点
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(n)**

### 知识点

### 优化
进阶需要O(1)的空间复杂度


## 快慢指针
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode* head) {
        if (head == nullptr || head->next==nullptr || head->next->next==nullptr) {
            return false;
        }
        auto fast{head->next->next};
        auto slow{head->next};
        while (fast != nullptr && fast->next != nullptr) {
            if (fast == slow) {
                return true;
            }
            slow = slow->next;
            fast = fast->next;
            if (fast->next == nullptr) {
                return false;
            }
            fast = fast->next;
        }
        return false;
    }
};
```
一快一慢，若有环终究会相遇.
### 评估
时间复杂度 **O(n)**

空间复杂度 **O(1)**

### 知识点

### 优化