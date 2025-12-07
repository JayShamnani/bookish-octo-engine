# [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)

Given the <code>head</code> of a singly linked list, return <code>true</code> if it is a <button type="button" aria-haspopup="dialog" aria-expanded="false" aria-controls="radix-:r1k:" data-state="closed" class="">palindrome</button> or <code>false</code> otherwise.

**Example 1:** 
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;">

```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:** 
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;">

```
Input: head = [1,2]
Output: false
```

**Constraints:** 

- The number of nodes in the list is in the range <code>[1, 10^5]</code>.
- <code>0 <= Node.val <= 9</code>

**Follow up:**  Could you do it in <code>O(n)</code> time and <code>O(1)</code> space?

# Solution

## O(n) Space:

```py
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        # Create a NEW reversed copy of the list using r
        x = r = ListNode()

        # Reverse the ORIGINAL list using prev
        t = head
        prev = None

        # This loop performs two heavy operations:
        # (1) Builds a full reversed copy of the entire list
        # (2) Simultaneously reverses the original list in-place
        while t:
            # Create a new node for the copied list
            r.next = ListNode(t.val)
            r = r.next

            # Reverse the original list
            nxt = t.next
            t.next = prev
            prev = t
            t = nxt

        # x moves to the actual head of the copied list
        x = x.next

        # Compare reversed original (prev) with copied reversed list (x)
        while prev and x:
            if prev.val != x.val:
                return False
            prev = prev.next
            x = x.next

        return True
```

⏱ Time Complexity: O(n)

Traverse each node a constant number of times.

📦 Space Complexity: O(n)

Building a full extra linked list copy.

## O(1) Space Complexity

```py
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:

        # STEP 1: Find the middle using slow/fast pointers
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # STEP 2: Reverse only the second half of the list
        prev = None
        while slow:
            nxt = slow.next
            slow.next = prev
            prev = slow
            slow = nxt
        # Now prev is the head of the reversed second half

        # STEP 3: Compare first half and reversed second half
        left = head
        right = prev
        while left and right:
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True
```
