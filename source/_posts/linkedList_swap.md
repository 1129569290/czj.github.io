---
title: linkedlist-swap
date: 2020-08-25 17:30:40
tags:
categories:
- 算法题
- linkedList
---

这类题目大同小异，都是枚举要反转的这一段的节点前一个节点

## Leetcode24两两交换链表中的节点

```go
func swapPairs(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    dummy := &ListNode{-1,head}
    cur := dummy
    for cur !=nil && cur.Next != nil && cur.Next.Next != nil {
        a := cur.Next
        b := a.Next
        c := b.Next
        a.Next = c
        cur.Next = b
        b.Next = a
        cur = a
    }
    return dummy.Next
}
```

## Leetcode25K个一组反转链表

```cpp
    if(!head)return nullptr;
    ListNode *dummy = new ListNode(-1);
    for(auto p = dummy; ;){
        auto q = p;// p就是前一个节点
        for(int i = 0; q && i < k; i++)q = q ->next;
        if(!q)break;
        auto nex = q ->next; //下一段的第一个节点
        auto a = q -> next;
        auto tmp = a;
        auto b = a -> next;
        while(b != nex){
            auto c = b -> next;
            b -> next = a;
            a = b; 
            b = c;
        }
        p -> next = a;
        tmp -> next = nex;
        p = tmp;
    }
    return dummy ->next;
```

## Leetcode61旋转链表

k 可能很大，所以我们令 k=k%n，n是链表长度。

创建两个指针first, second，分别指向头结点，先让first向后移动 k 个位置，然后first和second同时向后移动，直到first走到链表最后一个元素。此时first指向链表末尾，second指向分界点。然后我们把链表从分界点处断开，然后把后半段接在前半段前面即可。

```cpp
    ListNode* rotateRight(ListNode* head, int k) {
        if(!head)return nullptr;
        int len = 0;
        ListNode *p = head;
        while(p)p = p -> next,len++;
        k %= len;
        if(!k) return head;
        ListNode *fast = head, *slow = head;
        while(k-- && fast)fast = fast -> next;
        while(fast -> next){
            fast = fast -> next;
            slow = slow -> next;
        }
        fast -> next = head;
        head = slow -> next;
        slow -> next = nullptr;
        return head;
    }



```
