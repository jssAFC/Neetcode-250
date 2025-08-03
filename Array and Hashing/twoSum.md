# Two Sum Problem

Check two numbers that add up to the target.

## Brute Force Approach

Use a nested loop to check every pair of numbers.

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }
}
```

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)

## Better Approach

Sort the array and use two pointers to find a pair that sums to the target.

```java
public class Solution {
    public boolean twoSum(int[] nums, int target) {
        Arrays.sort(nums);
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) {
                return true;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return false;
    }
}
```

**Time Complexity:** O(n log n)  
**Space Complexity:** O(1)

## Optimal Approach

Use a hashmap to store elements and check for the complement that adds up to the target.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{0, 0};
    }
}
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

In this approach, each element is added to a hashmap and we check if its complement (target - current element) already exists.