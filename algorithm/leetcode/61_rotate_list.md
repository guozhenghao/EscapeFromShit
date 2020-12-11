# Rotate List 旋转链表
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

**示例:**
```
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```

**题解:**
```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

 // 环形链表
func rotateRight(head *ListNode, k int) *ListNode {
	if head == nil || head.Next == nil || k == 0 {
		return head
	}
	length, nodeTemp := 1, head
	for nodeTemp.Next != nil {
		nodeTemp = nodeTemp.Next
		length++
	}
    nodeTemp.Next = head
    nodeTemp = head
    times := length-k%length
	for i := 1; i < times; i++ {
		nodeTemp = nodeTemp.Next
	}
    head = nodeTemp.Next
    nodeTemp.Next = nil
	return head
}
```