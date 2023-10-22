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

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS_HTML" async></script>

# 704 Binary Search 

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Solution**: The problem asks programmers to write a Binary Search Algorithm. This is a classic algorithm to find a specific value in ordered ascending array. Also, the array cannot contain duplicated elements because the algorithm can only return one label. The main idea of the algorithm is setting three pointers: <span style="background-color: yellow">Left</span>, <span style="background-color: yellow">Right</span>, and <span style="background-color: yellow">Middle</span> to point the different positions in the array. By comparing the middle value with target, we can move <span style="background-color: yellow">Left</span> or <span style="background-color: yellow">Right</span> cursors to decrease the size of searching range.

At here we use closed interval ([<span style="background-color: yellow">Left</span>, <span style="background-color: yellow">Right</span>]) to implement our algorithm. The first step is to set <span style="background-color: yellow">Left</span> = 0 which points the first element in the array, <span style="background-color: yellow">Right</span> = <span style="background-color: yellow">array size - 1</span> which points the last element in the array, and <span style="background-color: yellow">Middle</span> = <span style="background-color: yellow">array size / 2</span> which points the middle element in the array. Don't worry about the array that has even number of elements, we just need a value that close to the middle of the array. The element will be considered in the algorithm. 

To find the target value, we need to compare the middle element with our target. If middle element is larger than the target, we know that our target will not in the elements on the right side because they are all larger than the target. Thus, we need to adjust the <span style="background-color: yellow">Right</span> cursor to <span style="background-color: yellow">Middle -1</span> position because the middle element is already considered. The theorem can also apply when the middle element is smaller than the target. In this situation, we need to move our <span style="background-color: yellow">Left</span> cursor to <span style="background-color: yellow">Middle + 1</span> position. Then, we reset our <span style="background-color: yellow">Middle</span> cursor to the middle of new range 

(Middle = (Right + Left) / 2).

The stop condition is <span style="background-color: yellow">Left</span> > <span style="background-color: yellow">Right</span>. The reason is that when <span style="background-color: yellow">Left</span> < <span style="background-color: yellow">Right</span>, the searching is not completed, we are still finding the target. When <span style="background-color: yellow">Left</span> == <span style="background-color: yellow">Right</span>, the <span style="background-color: yellow">Middle</span> cursor will be assigned to the same value as <span style="background-color: yellow">Left</span> and <span style="background-color: yellow">Right</span>. That is the last value we need to compare. When <span style="background-color: yellow">Left</span> > <span style="background-color: yellow">Right</span>, all elements in the array is accessed and we don't find our target. The target is not in the array so that the loop is over. Since the algorithm only check the half of the entire array, time complexity is `O(logn)`. 

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

