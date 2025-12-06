# [953. Verifying an Alien Dictionary](https://leetcode.com/problems/verifying-an-alien-dictionary/description/)

In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different <code>order</code>. The <code>order</code> of the alphabet is some permutation of lowercase letters.

Given a sequence of <code>words</code> written in the alien language, and the <code>order</code> of the alphabet, return <code>true</code> if and only if the given <code>words</code> are sorted lexicographically in this alien language.

**Example 1:** 

```
Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
```

**Example 2:** 

```
Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
```

**Example 3:** 

```
Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character (<a href="https://en.wikipedia.org/wiki/Lexicographical_order" target="_blank">More info</a>).
```

**Constraints:** 

- <code>1 <= words.length <= 100</code>
- <code>1 <= words[i].length <= 20</code>
- <code>order.length == 26</code>
- All characters in <code>words[i]</code> and <code>order</code> are English lowercase letters.

# Solution

```py
class Solution:
    def isAlienSorted(self, words: List[str], order: str) -> bool:
        # Create a mapping from each character in the alien alphabet
        # to its rank (index). This lets us compare characters quickly.
        rank = {c: i for i, c in enumerate(order)}

        # Compare each adjacent pair of words
        for i in range(1, len(words)):
            f = True   # Flag that checks if all compared chars so far are equal

            # Compare characters of the previous and the current word
            # zip() stops at the length of the shorter word
            for c1, c2 in zip(words[i - 1], words[i]):

                # If characters differ at this position, this determines the order
                if c1 != c2:

                    # If previous word's char ranks *after* current word's char → not sorted
                    if rank[c1] > rank[c2]:
                        return False

                    # If previous word's char ranks *before* current → order is correct
                    # Break because no further comparison is needed
                    if rank[c1] < rank[c2]:
                        f = False
                        break

            # If f is still True, it means:
            # - all characters matched in the zipped comparison, OR
            # - words share a prefix up to the shorter length
            # In this case, the shorter word must come first (e.g., "app" < "apple")
            if f and len(words[i - 1]) > len(words[i]):
                return False

        # If no invalid ordering was found, the words are alien-sorted
        return True
```
