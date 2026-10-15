---
lc-id: 1
lc-slug: two-sum
lc-title: Two Sum
lc-difficulty: Easy
lc-url: https://leetcode.com/problems/two-sum/
lc-status: accepted
lc-language: python3
aliases:
  - Two Sum
  - "1"
tags:
  - lc/easy
  - lc/array
  - lc/hash-table
---
# Two Sum
## Problem
You are given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```text
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```text
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**

-   `2 <= nums.length <= 10⁴`
-   `-10⁹ <= nums[i] <= 10⁹`
-   `-10⁹ <= target <= 10⁹`
-   **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than `O(n²)` time complexity?

## Code

```leetcode-solve
# Written by ChatGPT (Obsidian Copilot).
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        seen = {}

        for index, number in enumerate(nums):
            complement = target - number
            if complement in seen:
                return [seen[complement], index]
            seen[number] = index

        return []  # Unreachable when the input has the guaranteed solution.
```

## Notes
