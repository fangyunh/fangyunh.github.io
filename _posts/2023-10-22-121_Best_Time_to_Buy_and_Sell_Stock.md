---
layout:     post
title:      Best Time to Buy and Sell Stock
subtitle:   LeetCode 121 Best Time to Buy and Sell Stock
date:       2023-10-221
author:     FYH
header-img: img/post-bg-lc.jpg
catalog: true
tags:
    - LeetCode
---

# 121. Best Time to Buy and Sell Stock

Question: You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day. You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock. Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

Solution: During the loop, the program should record the minimum price and maximum profit and update them in each iteration. Hence, our minimum price keeps minimum and maximum profit keeps maximum. The time complexity is $O(n)$ which is efficient, but it costs a lot of space complexity to store values.

```C++
//C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minp = prices[0];    //min price
        int maxp = 0;            //max profit

        for (int i=1; i<prices.size(); ++i) { 
            if (prices[i] < minp) {
                minp = prices[i];
            }
            if (prices[i]-minp > maxp) {
                maxp = prices[i] - minp;
            }
        }
        return maxp;
    }
};
```

