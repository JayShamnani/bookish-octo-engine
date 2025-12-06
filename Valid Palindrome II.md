# [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/description/)

Given a string <code>s</code>, return <code>true</code> if the <code>s</code> can be palindrome after deleting **at most one**  character from it.

**Example 1:** 

```
Input: s = "aba"
Output: true
```

**Example 2:** 

```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

**Example 3:** 

```
Input: s = "abc"
Output: false
```

**Constraints:** 

- <code>1 <= s.length <= 10^5</code>
- <code>s</code> consists of lowercase English letters.

# Solution

## Brute Force
```py
class Solution:
    def validPalindrome(self, s: str) -> bool:
        # Quick check: if the whole string is already a palindrome, return True
        if s == s[::-1]:
            return True
        
        # This loop tries removing EACH character one-by-one
        # and checks if the remaining string is a palindrome.
        # This is slow because:
        # 1. There are n iterations
        # 2. Each substring slice s[:i] + s[i+1:] creates a NEW string of size O(n)
        # 3. Checking palindrome ls == ls[::-1] is another O(n)
        # So worst-case time = O(n^2)
        for i in range(len(s)):
            ls = s[:i] + s[i + 1:]  # O(n) slicing
            if ls == ls[::-1]:     # O(n) palindrome check
                return True        # Total overall = O(n^2)
        
        return False
```

## Optimal Solution

```py
class Solution:
    def validPalindrome(self, s: str) -> bool:

        # Helper to check if substring s[l:r+1] is a palindrome
        def is_pal(l, r):
            # Standard two-pointer palindrome check
            while l < r:
                if s[l] != s[r]:
                    return False
                l += 1
                r -= 1
            return True

        l, r = 0, len(s) - 1

        while l < r:
            if s[l] != s[r]:
                # Mismatch found — we can delete at most ONE character.
                # Option 1: delete character at 'l'  -> check s[l+1 : r]
                # Option 2: delete character at 'r'  -> check s[l : r-1]
                # Only one of these needs to work.
                return is_pal(l + 1, r) or is_pal(l, r - 1)

            # If characters match, move inward
            l += 1
            r -= 1
        
        # If entire loop finishes, it’s already a palindrome
        return True
```
