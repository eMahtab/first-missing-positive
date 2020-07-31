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
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
       if(nums == null || nums.length == 0)
           return 1;
        int n = nums.length;
        boolean containsOne = false;
        
        // Step 1 : Sets the containsOne flag to true if input array contains 1 ,
        // also sets all the negative numbers, zero and number's greater than n, to 1 
        // Make sure you don't mess up the order of statements
        for(int i = 0; i < n; i++) {
            if(nums[i] == 1) 
                containsOne = true; 
            else if(nums[i] <= 0 || nums[i] > n)
                nums[i] = 1;
        }
        
        // if array doesn't contains 1, the first missing positive will be 1
        if(!containsOne) return 1;
        
        // Step 2 : This step marks the number we have seen, by setting its index 
        // position to a negative number 
        // e.g. if nums[i] = 7, since 7 should come at index 6 (that's why - 1, array indexes starts with 0)
        // we mark nums[6] = nums[6] * -1 (if nums[6] was not already negative)
        for(int i = 0; i < n; i++) {
            int index = Math.abs(nums[i]) - 1;
            // if its already negative, we don't do anything
            if(nums[index] > 0)
                nums[index] *= -1;
        }
        
        // Step 3 : Finally, look for a non negative number in the array
        // If we find an index i, such that nums[i] is positive, that means
        // we didn't see the number which should come at this index i
        // the number that should come at index i should be i+1, so we return i+1
        for(int i = 0; i < n; i++) {
            if(nums[i] > 0) return i + 1;
        }  
        
        // If we reach here it means, original input array had all the positive numbers 
        // from 1 to n, so the first missing positive number will be n + 1
        return n + 1;
    }
}
```

### Tip :
Run your code through some examples :
```
[1, 2, 3],
[1, 2, 2],
[1, 3, 3],
[2, 2, 2],
[4, 5, 1]
```
# References :
https://www.youtube.com/watch?v=9SnkdYXNIzM
