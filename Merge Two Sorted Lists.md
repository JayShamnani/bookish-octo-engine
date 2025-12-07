# [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)

You are given the heads of two sorted linked lists <code>list1</code> and <code>list2</code>.

Merge the two lists into one **sorted**  list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

**Example 1:** 

<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" style="width: 662px; height: 302px;">

```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

**Example 2:** 

```
Input: list1 = [], list2 = []
Output: []
```

**Example 3:** 

```
Input: list1 = [], list2 = [0]
Output: [0]
```

**Constraints:** 

- The number of nodes in both lists is in the range <code>[0, 50]</code>.
- <code>-100 <= Node.val <= 100</code>
- Both <code>list1</code> and <code>list2</code> are sorted in **non-decreasing**  order.

# Solution

```py

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        # Create a dummy node so we don't have to handle special cases for head
        res = t = ListNode()

        # Compare nodes from both lists while both are non-empty
        # Always attach the smaller one to the result list
        while l1 and l2:
            if l1.val <= l2.val:
                # Attach l1 node value to the merged list
                t.next = ListNode(l1.val)
                l1 = l1.next       # Move l1 forward
            else:
                # Attach l2 node value to the merged list
                t.next = ListNode(l2.val)
                l2 = l2.next       # Move l2 forward
            
            t = t.next             # Move the tail pointer forward

        # If any nodes are left in l1, attach all of them
        while l1:
            t.next = ListNode(l1.val)
            l1 = l1.next
            t = t.next

        # If any nodes are left in l2, attach all of them
        while l2:
            t.next = ListNode(l2.val)
            l2 = l2.next
            t = t.next

        # res.next is the actual merged sorted list
        return res.next


```

"""
EXPLANATION:
-----------
This algorithm merges two sorted linked lists into a new sorted linked list.
It works exactly like merging step in merge sort:
- Compare the smallest available elements from both lists.
- Pick the smaller one and attach it to the result.
- Continue until one list finishes.
- Append the rest from the other list.

TIME COMPLEXITY:
----------------

O(n + m)

Where:
- n = number of nodes in l1
- m = number of nodes in l2
- We visit each node exactly once.

SPACE COMPLEXITY:
-----------------

O(n + m)

Because we are creating a NEW linked list with new ListNode objects.
(If we reused nodes instead of creating new ones, space would be O(1).)
"""
