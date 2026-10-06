# 1. Two Sum

## Problem statement

![Problem 1 statement](../img/1.png)

## First intuition: Brute Force

The **Two Sum** problem is the first problem that appears on LeetCode when you arrive on the platform. Obviously, it's a beginner-level problem, and because of that, it also accepts beginner-level answers.

In my case, it was the first problem I solved on LeetCode. It was an opportunity to understand that, as a beginner, the first solution we have in mind is, most of the time, not the most optimized.

So when I first read the problem statement, here is the algorithm I had in mind:

1. We use an index `i` to iterate through the list
2. For each `nums[i]` we are iterating through all the following entries of the list, with an index `j`, and compute the sum each time
3. If we have a sum which is equal to `target`, we return `[i, j]`
4. Otherwise, we increment `i` and do the process again until we've reached the end of the list

In this case, the number of operations for a list of size **n** is: n+(n-1)+(n-2)+...+1 = (n(n+1))/2 = **n²/2 + n/2**.
So the time complexity is **O(n²)**, which is not ideal.

Here is the code I submitted on LeetCode:

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        nums_size = len(nums)
        for i in range(nums_size):
            for j in range(i + 1, nums_size):
                sum = nums[i] + nums[j]
                if sum == target:
                    return [i, j]
        return [] # Shouldn't happen
```

Somehow, it passed all the test cases. But we can solve this problem in a more efficient way.

## Best solution: Hash map

We can use a [map](https://www.geeksforgeeks.org/dsa/introduction-to-map-data-structure/). Each entry will have, as a key, an item of the list and, as a value, the index of the item in the list.

For example, if we have `nums = [7, 8, -4]`, we will have `map[7]` equal to `0`, `map[8]` equal to `1`, and `map[-4]` equal to `2`.

For maximum efficiency, we will fill this map while we are iterating through the list.

The algorithm is the following:

1. We use an index `i` to iterate through the list
2. We check if the map contains the key `target - nums[i]`
3. If it's the case, we have a pair whose sum is equal to `target`, and we return `[map[target - nums[i]], i]`
4. Otherwise, we store the current item in the map, with its index, increment `i`, and repeat the process until we reach the end of the list

We are iterating only one time through each item, so here the time complexity is **O(n)**, which is far better.

Here is the code that implements this algorithm:

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        hashMap = {}
        for i in range(len(nums)):
            diff = target - nums[i]
            if diff in hashMap:
                return [hashMap[diff], i]
            hashMap[nums[i]] = i
        return [] # Shouldn't happen
```

## Conclusion

Here we've seen that, even for a simple problem, it's important to consider multiple options and see which one is the fastest. Also, having a good knowledge of data structures can be the key to finding an efficient solution to a problem (here, the hash map).