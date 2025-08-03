## Description
Check if there are any duplicate elements in an integer array.

---

### Brute Force Approach

Use a nested loop to compare each element with the others.

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == num) return true;
            }
        }
        return false;
    }
}
```

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)

---

### Better Approach 

Sort the array and check if any two adjacent elements are equal.

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == nums[i + 1]) return true;
        }
        return false;
    }
}
```

**Time Complexity:** O(n log n)  
**Space Complexity:** O(n)

---

### Optimal Approach

Use a hashmap to check if an element already exists while iterating. Alternatively, you could use a hashset and compare the sizes.

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i])) return true;
            map.put(nums[i], 1);
        }
        return false;
    }
}
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---



