# 链表代码随想录练习

## 203.移除链表元素
这道题没什么难度，记住不要丢失节点就行了

## 206.翻转链表
```cpp
ListNode* reverseList(ListNode* head) {
        ListNode* front = nullptr;
        while(head != nullptr){
            ListNode* temp = head->next;
            ListNode* temp1 = head;
            head->next = front;
            front = temp1;
            head = temp;
        }
        return front;
    }
```
翻转链表就是双指针法的翻版，主意好两个指针和循环结束的判定条件就行了

## 24.两两交换列表中的节点
```cpp
ListNode* swapPairs(ListNode* head) {
        if(head == nullptr || head->next == nullptr) return head;
        ListNode* ans = head->next;
        ListNode* front = new ListNode(0, head);
        ListNode* back = head->next;
        while(head != nullptr && head->next != nullptr){
            front->next = head->next;
            back = head->next->next;
            head->next->next = head;
            head->next = back;
            front = head;
            head = back;
        }
        return ans;
    }
```
这道题相当于是翻转链表的进阶，我是使用了记录两个一组之后前后两个指针的方式来进行翻转

## 19.删除链表的倒数第N个节点
```cpp
 ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* temp = head;
        for(int i = 1; i < n; i++){
            head = head->next;
        }
        ListNode* front = new ListNode(0, temp);
        ListNode* dummyhead = front;
        while(head != nullptr && head->next != nullptr){
            head = head->next;
            temp = temp->next;
            front = front->next;
        }
        front->next = temp->next;
        delete temp;
        return dummyhead->next;
    }
```
这道题有一个比较讨巧的方法，就是把题目给出的n当作距离来看，也就是和链表表尾的距离，那么用两个指针就行了，一个指向现在的节点，一个指向距离n的节点，距离n的节点遍历到链表尾就行了

## 142.环形链表
```cpp
 ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast != NULL && fast->next != NULL){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow){
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while(index1 != index2){
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index1;
            }
        }
        return NULL;
    }
```
环形链表这道题一开始没想出来，看了题解才有点思路。
总体思路是快慢指针
通过记录快指针和慢指针相遇的位置来计算环形链表的进入节点。
这种快慢指针图论里面可能也有用
相遇时： slow指针走过的节点数为: x + y， fast指针走过的节点数：x + y + n (y + z)，n为fast指针在环内走了n圈才遇到slow指针， （y+z）为 一圈内节点的个数A。

因为fast指针是一步走两个节点，slow指针一步走一个节点， 所以 fast指针走过的节点数 = slow指针走过的节点数 * 2：

(x + y) * 2 = x + y + n (y + z)

两边消掉一个（x+y）: x + y = n (y + z)

因为要找环形的入口，那么要求的是x，因为x表示 头结点到 环形入口节点的的距离。

所以要求x ，将x单独放在左面：x = n (y + z) - y ,

再从n(y+z)中提出一个 （y+z）来，整理公式之后为如下公式：x = (n - 1) (y + z) + z 注意这里n一定是大于等于1的，因为 fast指针至少要多走一圈才能相遇slow指针。

这个公式说明什么呢？

先拿n为1的情况来举例，意味着fast指针在环形里转了一圈之后，就遇到了 slow指针了。

当 n为1的时候，公式就化解为 x = z，

这就意味着，从头结点出发一个指针，从相遇节点 也出发一个指针，这两个指针每次只走一个节点， 那么当这两个指针相遇的时候就是 环形入口的节点。

也就是在相遇节点处，定义一个指针index1，在头结点处定一个指针index2。

让index1和index2同时移动，每次移动一个节点， 那么他们相遇的地方就是 环形入口的节点。   ---代码随想录摘录


