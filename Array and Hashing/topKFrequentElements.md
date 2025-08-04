# Top K Frequent Elements

**Description:** In this question we have to find the top k frequently occurring elements in an array.

## Brute Force 1

In this approach we will use a sorting algorithm. First we will create a hashmap and put all the occurring elements.

Then we will create a list and put all the elements from the hashmap into it. Then we are going to sort the list using a comparator function.

Once done we will extract the first k elements from the list and return them.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i : nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }

        List<int[]> list = new ArrayList<>();
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            list.add(new int[]{entry.getKey(), entry.getValue()});
        }

        list.sort((a, b) -> b[1] - a[1]);

        int[] arr = new int[k];
        for (int i = 0; i < k; i++) {
            arr[i] = list.get(i)[0];
        }

        return arr;
    }
}
```

**Time Complexity:** O(n log n) if all n elements are distinct, else O(m + m log m) where m are distinct elements  
**Space Complexity:** O(n) or O(m)

## Brute Force 2

Using a priority queue. We will put the elements in a hashmap and then use a priority queue to store the int[] key-value pair of the hashmap. We are going to add a comparator function on the queue which sorts the elements based on the occurrence of the value. Once done we will remove the top k elements from the priority queue.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i : nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }

        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[1] - a[1]);
        for (int key : map.keySet()) {
            pq.add(new int[]{key, map.get(key)});
        }

        int[] ans = new int[k];
        for (int i = 0; i < k; i++) {
            int[] temp = pq.poll(); // operation for removing an element from the top is log m
            ans[i] = temp[0];
        }

        return ans;
    }
}
```

**Time Complexity:** O(n log n) or O(n + m log m)  
**Space Complexity:** O(n) or O(m)

## Optimal Solution

In this approach we are going to use bucket sort.

First we will create a hashmap of numbers and their corresponding frequencies. Then we will create an array of type List of length nums.length + 1. Then we are going to iterate over the hashmap and for every corresponding element, we are going to store the key in the frequency index of the array. That is, we are going to store elements by the frequency with which they are occurring.

Once done we will iterate from the end of the array and iterate over every list in it. We will keep adding the elements in the result array until we reach the limit of k elements. Once we reach k elements, we will stop.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i : nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }

        List<Integer>[] list = new List[nums.length + 1];
        for (int i = 0; i < nums.length + 1; i++) 
            list[i] = new ArrayList<>();

        for (Map.Entry<Integer, Integer> m : map.entrySet()) {
            list[m.getValue()].add(m.getKey());
        }

        int index = 0;
        int[] result = new int[k];
        for (int i = list.length - 1; i >= 0; i--) {
            for (int j : list[i]) {
                result[index++] = j;
                if (index == k) 
                    return result;
            }
        }

        return result;
    }
}
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)