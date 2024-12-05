# Intuition

To remove nodes from a linked list whose values exist in a given array, we can use a set for efficient lookups. By iterating through the linked list and using the set to check for values to be removed, we can modify the list in place.

<p>&nbsp;</p>

# Approach: HashSet

## Explanation:

1. **Create a Set**:

   - Convert the given array `nums` into an `unordered_set` for O(1) average-time complexity lookups.

2. **Initialize a Dummy Node**:

   - Use a dummy node that points to the head of the linked list. This helps simplify edge cases where the head itself needs to be removed.

3. **Iterate Through the Linked List**:

   - Use a pointer `curr` initialized to the dummy node.
   - Traverse the list using `curr`. For each node, check if the next node's value exists in the set:
     - If it does, skip the next node by updating `curr->next` to `curr->next->next`.
     - Otherwise, move the `curr` pointer to the next node.

4. **Return the Modified List**:
   - Return `dummy.next` which points to the new head of the modified list.

## Complexity

- Time complexity: $O(n + m)$, where `n` is the length of the linked list and `m` is the length of the array `nums`.
- Space complexity: $O(m)$.

## Code

### C++

```cpp
class Solution {
public:
    ListNode* modifiedList(vector<int>& nums, ListNode* head) {
        unordered_set<int> us(nums.begin(), nums.end());

        ListNode dummy(0, head);
        ListNode *curr = &dummy;

        while (curr->next) {
            if (us.find(curr->next->val) != us.end()) {
                curr->next = curr->next->next;
            }
            else {
                curr = curr->next;
            }
        }

        return dummy.next;
    }
};
```

### Go

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func modifiedList(nums []int, head *ListNode) *ListNode {
    set := make([]bool, 100_001)
    for _, num := range nums {
        set[num] = true
    }

    dummy := &ListNode{Next: head}
    current := dummy
    for current.Next != nil {
        if set[current.Next.Val] {
            current.Next = current.Next.Next
        } else {
            current = current.Next
        }
    }
    return dummy.Next
}
```

### Java
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode modifiedList(int[] nums, ListNode head) {
        Set<Integer> lookUpSet = new HashSet<>();
        for (int num : nums) {
            lookUpSet.add(num);
        }

        ListNode dummy = new ListNode(0, head);
        ListNode current = dummy;

        while (current.next != null) {
            if (lookUpSet.contains(current.next.val)) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }

        return dummy.next;
    }
}
```