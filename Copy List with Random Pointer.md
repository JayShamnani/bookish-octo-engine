# [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

A linked list of length <code>n</code> is given such that each node contains an additional random pointer, which could point to any node in the list, or <code>null</code>.

Construct a <a href="https://en.wikipedia.org/wiki/Object_copying#Deep_copy" target="_blank">**deep copy** </a> of the list. The deep copy should consist of exactly <code>n</code> **brand new**  nodes, where each new node has its value set to the value of its corresponding original node. Both the <code>next</code> and <code>random</code> pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list** .

For example, if there are two nodes <code>X</code> and <code>Y</code> in the original list, where <code>X.random --> Y</code>, then for the corresponding two nodes <code>x</code> and <code>y</code> in the copied list, <code>x.random --> y</code>.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of <code>n</code> nodes. Each node is represented as a pair of <code>[val, random_index]</code> where:

- <code>val</code>: an integer representing <code>Node.val</code>
- <code>random_index</code>: the index of the node (range from <code>0</code> to <code>n-1</code>) that the <code>random</code> pointer points to, or <code>null</code> if it does not point to any node.

Your code will **only**  be given the <code>head</code> of the original linked list.

**Example 1:** 
<img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e1.png" style="width: 700px; height: 142px;">

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**Example 2:** 
<img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e2.png" style="width: 700px; height: 114px;">

```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```

**Example 3:** 

**<img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e3.png" style="width: 700px; height: 122px;">** 

```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```

**Constraints:** 

- <code>0 <= n <= 1000</code>
- <code>-10^4 <= Node.val <= 10^4</code>
- <code>Node.random</code> is <code>null</code> or is pointing to some node in the linked list.

# Solution

```py
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        # Dummy nodes for constructing the copied list
        copy = x = y = c = Node(0, None, None)

        # fr, v pointers to traverse the original list
        fr = v = head

        # hmap   : maps (node.val, node.next) → index
        # tmap   : maps index → newly created node (value only, no links yet)
        # copied_map : will map index → final copied node in the constructed list
        hmap = dict()
        tmap = dict()
        copied_map = dict()

        # First pass: store index of each node using unique key (value + next pointer)
        idx = 0
        while v:
            hmap[(v.val, v.next)] = idx     # store the index of this node
            tmap[idx] = Node(v.val, None, None)  # create a node copy (no next/random yet)
            v = v.next
            idx += 1

        # Second pass: capture all random-pointer targets as integer indices
        rand_list = list()
        while fr:
            random = None
            if fr.random:
                # convert random pointer into index using hmap
                random = hmap[(fr.random.val, fr.random.next)]
            rand_list.append(random)
            fr = fr.next

        # Third pass: build the full next-linked list using the tmap nodes
        for i in range(idx):
            c.next = Node(tmap[i].val, None, None)  # link the actual node
            c = c.next

        # Fourth pass: map index → actual copied node (in the final next-linked list)
        for i in range(idx):
            copied_map[i] = y.next
            y = y.next

        # Fifth pass: assign random pointers using copied_map and rand_list
        for i in range(idx):
            if rand_list[i] is not None:
                x.next.random = copied_map[rand_list[i]]
            x = x.next

        # Return head of the deep-copied list
        return copy.next

```


⏱️ Time Complexity
---

Time: O(N)

Each of the five passes over the list is linear:

Indexing nodes → O(N)

Collecting random pointers → O(N)

Building the next-connected list → O(N)

Mapping indices to copied nodes → O(N)

Assigning random pointers → O(N)

So total time = O(N).

💾 Space Complexity
---

Space: O(N)

The solution uses:

hmap → O(N)

tmap → O(N)

rand_list → O(N)

copied_map → O(N)

Thus total additional space = O(N).
