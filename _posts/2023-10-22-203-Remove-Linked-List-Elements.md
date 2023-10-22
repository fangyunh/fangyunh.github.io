---
layout:     post
title:      Remove Linked List Elements
subtitle:   LeetCode 203 Remove Linked List Elements
date:       2023-10-22
author:     FYH
header-img: img/post-bg-lc.jpg
catalog: true
tags:
    - LeetCode
---

# 203 Remove Linked List Elements

Remove all elements from a linked list of integers that have value **val**.



**Solution**: The problem asks programmers to implement a typical linked list function. We discuss one-way linked list here. This is the simplest linked list struct that has two properties: a ==value== and a pointer which points the next node address (==next==). Since it is one-way linked list, we can only go over the linked list from head to tail. We cannot access nodes in inverse order. If we want to do that we need to use two-way linked list which contains one more property to store the address of previous node. 

The principle of remove an element from linked list is to change the address stored in its previous node's next pointer. Hence, when we access the linked list, we will jump over the element we want to delete. 

For this question, we need to consider one more possible circumstance: ==val == header->val==. To handle this special circumstance, we can create a fake header called ==dummyNode== and store use its ==next== pointer to point ==header==. Thus, ==header== turns to a normal node in our linked list. Remember, if you use C/C++, using ==free== or ==delete== to free the space that you deleted and ==dummyNode== in the end is a good habit since C/C++ cannot automatically free them. Finally, we return the ==dummyNode->next== because that is our new linked list's header.

```c
// C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* removeElements(struct ListNode* head, int val){
    struct ListNode* nextNode;
    struct ListNode* dummyNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    
    dummyNode->next = head;
    nextNode = dummyNode;

    while (nextNode->next != NULL) {
        if (nextNode->next->val == val) {
            struct ListNode* tmpNode;
            tmpNode = nextNode->next;
            nextNode->next = tmpNode->next;
            free(tmpNode);
        } else {
            nextNode = nextNode->next;
        }

    }
    head = dummyNode->next;
    free(dummyNode);

    return head;
}
```

