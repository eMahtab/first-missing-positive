# First Missing Positive
## https://leetcode.com/problems/first-missing-positive

Given an unsorted integer array, find the smallest missing positive integer.
```
Example 1:

Input: [1,2,0]
Output: 3

Example 2:

Input: [3,4,-1,1]
Output: 2

Example 3:

Input: [7,8,9,11,12]
Output: 1
```
**Note: Your algorithm should run in O(n) time and uses constant extra space.**

# Implementation 1 : O(n) Space
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        for(int num : nums)
            set.add(num);
        int i = 1;
        for(; i <= nums.length; i++) {
            if(!set.contains(i))
                 return i;
        }
       return i; 
    }
}
```

# Implementation 2 : O(1) Constant Space
