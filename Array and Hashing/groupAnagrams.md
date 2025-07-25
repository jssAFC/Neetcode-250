# Problem Statement
Given a list of strings, return all groups of anagrams together.

Anagrams are words or phrases formed by rearranging the letters of another, for example, "eat" and "tea".

There are two possible approaches to solve this problem:

## 1) Brute Force (Sorting)

For every string in the array, sort the characters and use the sorted string as the key in a HashMap. This groups all anagrams together.

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] arr) {
        Map<String, List<String>> map = new HashMap<>();

        for (String s : arr) {
            char[] charArray = s.toCharArray();
            Arrays.sort(charArray);
            String sorted = new String(charArray);

            List<String> group = map.getOrDefault(sorted, new ArrayList<>());
            group.add(s);
            map.put(sorted, group);
        }
        return new ArrayList<>(map.values());
    }
}
```

**Time Complexity:** O(m * nlogn)  
- m = number of strings  
- n = average length of a string (sorting each string)

**Space Complexity:** O(m * n)  
- Storing each string in the map.

## 2) Optimal Approach (Counting Characters)

Instead of sorting, count the frequency of each letter (assuming only lowercase letters). Use the count array converted to a string as the key in the HashMap.

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] arr) {
        Map<String, List<String>> map = new HashMap<>();

        for (String s : arr) {
            int[] count = new int[26];
            for (char c : s.toCharArray()) {
                count[c - 'a']++;
            }
            String key = Arrays.toString(count);
            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```

**Time Complexity:** O(n * m)  
- n = number of strings  
- m = average length of a string (counting characters)

**Space Complexity:** O(n * m)  
- Storing each string and the count arrays in the map.