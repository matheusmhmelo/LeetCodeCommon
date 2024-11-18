You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

Example 1:

Input: head = [1,2,3,4]
Output: [1,4,2,3]

Example 2:

Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]

###########################

/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reorderList(head *ListNode)  {
    if head == nil || head.Next == nil {
        return
    }

    var prev *ListNode
    curr := head
    for curr.Next != nil {
        prev = curr
        curr = curr.Next
    }

    if prev != nil {
        prev.Next = nil
    }

    reorderList(head.Next)

    curr.Next = head.Next
    head.Next = curr
}

