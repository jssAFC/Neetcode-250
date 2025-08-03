# Anagrams
Anagrams are words that can be transformed into each other by rearranging their characters.

## Brute Force Approach
Convert both strings to character arrays, sort them, and then compare them element by element.

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length())
            return false;

        char[] s1 = s.toCharArray();
        char[] s2 = t.toCharArray();

        Arrays.sort(s1);
        Arrays.sort(s2);

        for (int i = 0; i < s1.length; i++) {
            if (s1[i] != s2[i])
                return false;
        }

        return true;
    }
}
```
**Time Complexity:** O(n log n) + O(mlog m)  
**Space Complexity:** O(n + m)

## Better Approach
Use hash maps to count characters. Increment counts for the first string and decrement for the second. If any count goes negative or is not zero at the end, return false.

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) 
            return false;
        
        Map<Character, Integer> map = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        for (int i = 0; i < t.length(); i++) {
            char ch = t.charAt(i);
            if (!map.containsKey(ch) || map.get(ch) == 0) {
                return false;
            }
            map.put(ch, map.get(ch) - 1);
        }

        for (int count : map.values()) {
            if (count != 0) 
                return false;
        }
        
        return true;
    }
}
```
**Time Complexity:** O(n + m)  
**Space Complexity:** O(n + m) or O(1) if the character set is fixed.

## Optimal Approach
Use an array as a hash table for a fixed set of characters (assumes only lowercase letters).

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) 
            return false;

        int[] arr = new int[26];

        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i) - 'a']++;
        }

        for (int i = 0; i < t.length(); i++) {
            arr[t.charAt(i) - 'a']--;
        }

        for (int count : arr) {
            if (count != 0) 
                return false;
        }
        
        return true;
    }
}
```
**Time Complexity:** O(n)  
**Space Complexity:** O(1)
