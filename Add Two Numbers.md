# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)

You are given two **non-empty**  linked lists representing two non-negative integers. The digits are stored in **reverse order** , and each of their nodes contains a single digit. Add the two numbers and return the sumas a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:** 
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg" style="width: 483px; height: 342px;">

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:** 

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:** 

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:** 

- The number of nodes in each linked list is in the range <code>[1, 100]</code>.
- <code>0 <= Node.val <= 9</code>
- It is guaranteed that the list represents a number that does not have leading zeros.

# Solution

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        rem = 0                     # carry value (0 or 1 most of the time)
        res = t = ListNode()        # dummy node to simplify list building

        # Process both lists while they have nodes
        while l1 and l2:
            s = l1.val + l2.val + rem   # sum current digits + carry
            t.next = ListNode(s % 10)   # put the unit digit in the result
            rem = s // 10               # update carry
            l1 = l1.next                # move pointers
            l2 = l2.next
            t = t.next                  # move result pointer

        # If l1 is longer
        while l1:
            s = l1.val + rem
            t.next = ListNode(s % 10)
            rem = s // 10
            l1 = l1.next
            t = t.next

        # If l2 is longer
        while l2:
            s = l2.val + rem
            t.next = ListNode(s % 10)
            rem = s // 10
            l2 = l2.next
            t = t.next

        # If carry remains after finishing lists
        while rem:
            t.next = ListNode(rem)
            rem //= 10
            t = t.next

        return res.next               # skip dummy node
```
