### Description:

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 


### Examples (input --> output):

```

Example 1:


Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

```

### Constraints:

```
The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.
```

### Solutions

#### C 

```C
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
    struct ListNode* dummy = (struct ListNode*)malloc(sizeof(struct ListNode));
    struct ListNode* current = dummy;
    int carry = 0;

    while (l1 || l2 || carry) {
        int x = (l1) ? l1->val : 0;
        int y = (l2) ? l2->val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        current->next = (struct ListNode*)malloc(sizeof(struct ListNode));
        current->next->val = sum % 10;
        current->next->next = NULL;
        current = current->next;

        if (l1) l1 = l1->next;
        if (l2) l2 = l2->next;
    }

    return dummy->next;
}

```

#### JS

```JS
var addTwoNumbers = function(l1, l2) {
    let dummy = new ListNode(0);
    let current = dummy;
    let carry = 0;
    while (l1 || l2) {
        let x = (l1) ? l1.val : 0;
        let y = (l2) ? l2.val : 0;
        let sum = carry + x + y;
        carry = Math.floor(sum / 10);
        current.next = new ListNode(sum % 10);
        current = current.next;
        if (l1) l1 = l1.next;
        if (l2) l2 = l2.next;
    }
    if (carry) {
        current.next = new ListNode(carry);
    }
    return dummy.next;
};

```

#### Java

```Java
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // Initialize a dummy node to act as the head of the resulting linked list
        ListNode dummy = new ListNode(0);
        // Current node in the new linked list
        ListNode current = dummy;
        // Initialize carry to 0
        int carry = 0;

        // Iterate through both linked lists
        while (l1 != null || l2 != null) {
            // Get the values of the current nodes (0 if the node is null)
            int x = (l1 != null) ? l1.val : 0;
            int y = (l2 != null) ? l2.val : 0;

            // Compute the sum of the values and the carry
            int sum = carry + x + y;
            // Update the carry for the next addition
            carry = sum / 10;
            // Create a new node with the digit value of the sum
            current.next = new ListNode(sum % 10);
            // Move to the next node in the new linked list
            current = current.next;

            // Move to the next nodes in the input linked lists
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        // If there is a carry left after the final addition, create a new node for it
        if (carry > 0) {
            current.next = new ListNode(carry);
        }

        // Return the next node of the dummy node, which is the head of the resulting linked list
        return dummy.next;
    }
}
```