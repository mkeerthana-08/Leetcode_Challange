# LeetCode Problem 169: Majority Element

## Problem Statement

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times.
You may assume that the majority element always exists in the array.

## Screenshot

![Accepted Solution](screenshots/ss.png)

**Runtime:** 0 ms (Beats 100.00%)  
**Memory:** 28.13 MB (Beats 62.64%)  
**Status:** Accepted ✅ (53/53 test cases passed)

## Examples

**Example 1:**

Input: nums = [3,2,3]

Output: 3

**Example 2:**

Input: nums = [2,2,1,1,1,2,2]

Output: 2

## ✅ Solution 1: Hash Table Approach

### Concept Used

- Array Traversal
- Hash Table (Frequency Counting)

### Solution Explanation

We use an unordered_map to store the frequency of each element.
While iterating through the array, we increment the count of each number.
If any number’s frequency becomes greater than n/2, we return it immediately.

### Step-by-Step Procedure

1. Create a hash map to store frequencies.
2. Traverse through each element in nums.
3. Increment its count in the map.
4. If count > n/2, return that element.

### C++ Implementation

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> count;
        int n = nums.size();
        for (int num : nums) {
            count[num]++;
            if (count[num] > n/2) return num;
        }
        return -1;
    }
};
```

### Performance

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

## ✅ Solution 2: Sorting Approach (Accepted)

### Concept Used

- Array
- Sorting

### Solution Explanation

If an element appears more than n/2 times,
after sorting the array, it must occupy the middle position.

So we:

1. Sort the array
2. Return element at index n/2

### C++ Implementation

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size()/2;
        return nums[n];
    }
};
```

### Performance

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

## ✅ Solution 3: Boyer–Moore Voting Algorithm (Optimal)

### Concept Used

- Greedy
- Voting Algorithm
- Constant Space Optimization

### Solution Explanation

This method maintains:

- A candidate element
- A counter

If counter becomes 0, we select a new candidate.
Matching elements increase the counter.
Different elements decrease the counter.

Since the majority element appears more than n/2 times,
it cannot be completely cancelled out.

### C++ Implementation

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = 0, count = 0;
        for (int num : nums) {
            if (count == 0) candidate = num;
            count += (num == candidate) ? 1 : -1;
        }
        return candidate;
    }
};
```

## Summary

| Approach | Time Complexity | Space Complexity | Notes |
|----------|----------------|------------------|-------|
| Hash Map | O(n) | O(n) | Easy but uses extra space |
| **Sorting** | **O(n log n)** | **O(1)** | **Simple logic (Accepted Solution)** |
| Boyer–Moore | O(n) | O(1) | Optimal approach |

The **Sorting approach** was used in the accepted solution shown above. While Boyer–Moore Voting Algorithm is more optimal with O(n) time complexity, the sorting approach is simpler to understand and implement, achieving 100% runtime performance.