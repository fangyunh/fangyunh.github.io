---
layout:     post
title:      Binary Search
subtitle:   LeetCode 704 Binary Search Solution
date:       2023-10-22
author:     FYH
header-img: img/post-bg-lc.jpg
catalog: true
tags:
    - LeetCode
---

# 704 Binary Search 

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Solution**: The problem asks programmers to write a Binary Search Algorithm. This is a classic algorithm to find a specific value in ordered ascending array. Also, the array cannot contain duplicated elements because the algorithm can only return one label. The main idea of the algorithm is setting three pointers: ==Left==, ==Right==, and ==Middle== to point the different positions in the array. By comparing the middle value with target, we can move ==Left== or ==Right== cursors to decrease the size of searching range.

At here we use closed interval ([==Left==, ==Right==]) to implement our algorithm. The first step is to set ==Left== = 0 which points the first element in the array, ==Right== = ==array size - 1== which points the last element in the array, and ==Middle== = ==array size / 2== which points the middle element in the array. Don't worry about the array that has even number of elements, we just need a value that close to the middle of the array. The element will be considered in the algorithm. 

To find the target value, we need to compare the middle element with our target. If middle element is larger than the target, we know that our target will not in the elements on the right side because they are all larger than the target. Thus, we need to adjust the ==Right== cursor to ==Middle -1== position because the middle element is already considered. The theorem can also apply when the middle element is smaller than the target. In this situation, we need to move our ==Left== cursor to ==Middle + 1== position. Then, we reset our ==Middle== cursor to the middle of new range 

($Middle = (Right + Left) / 2$).

The stop condition is ==Left== > ==Right==. The reason is that when ==Left== < ==Right==, the searching is not completed, we are still finding the target. When ==Left== == ==Right==, the ==Middle== cursor will be assigned to the same value as ==Left== and ==Right==. That is the last value we need to compare. When ==Left== > ==Right==, all elements in the array is accessed and we don't find our target. The target is not in the array so that the loop is over. Since the algorithm only check the half of the entire array, time complexity is `O(logn)`. 

```C
// C
int search(int* nums, int numsSize, int target){
    int mid = numsSize / 2;
    int start = 0;
    int end = numsSize - 1;
    while (start <= end) {
        if (target > nums[mid]) {
            start = mid + 1;
        } else if (target < nums[mid]) {
            end = mid - 1;
        } else {
            return mid;
        }

        mid = (end + start) / 2;
    }

    return -1;
    
}
```

