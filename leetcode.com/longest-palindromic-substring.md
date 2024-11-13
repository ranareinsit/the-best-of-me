### Description:

5. Longest Palindromic Substring

Given a string s, return the longest palindromic substring in s.

### Examples (input --> output):

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

```
Input: s = "cbbd"
Output: "bb"
```

### Constraints:

```
1 <= s.length <= 1000
s consist of only digits and English letters.
```

### Solutions

#### C 

```C
#include <string.h>
#include <stdlib.h>

char* longestPalindrome(char* s) {
    int start = 0, end = 0, len = strlen(s);
    if (len == 0) return "";

    int expand(char* s, int l, int r) {
        while (l >= 0 && r < len && s[l] == s[r]) l--, r++;
        return r - l - 1;
    }

    for (int i = 0; i < len; i++) {
        int len1 = expand(s, i, i);
        int len2 = expand(s, i, i + 1);
        int max_len = (len1 > len2) ? len1 : len2;
        if (max_len > end - start) {
            start = i - (max_len - 1) / 2;
            end = i + max_len / 2;
        }
    }

    char* result = (char*)malloc((end - start + 2) * sizeof(char));
    strncpy(result, s + start, end - start + 1);
    result[end - start + 1] = '\0';
    return result;
}

```

#### JS


Here’s a quick assessment of each option:







1. **Naive Solution (first)**: This approach has $O(n^3)$ complexity due to the nested loops and substring checking. Not efficient for large strings, so it’s the least optimal.
```JS
// naive
function longestPalindrome(s) {
    if (s.length < 3) return s[0] == s[1] ? s : s[0]
    let longest = s[0]
    let check = (s) => {
        for (let i = 0; i < Math.floor(s.length / 2); i++) {
            if (s[i] != s[s.length - i - 1]) return false
        }
        return true
    }
    for (let i = 0; i < s.length - 1; i++) {
        let j = Math.max(longest.length, i + 1)
        while (j < s.length) {
            let current = s.slice(i, j + 1)
            if (check(current) && longest.length < current.length) {
                longest = current
            }
            j++
        }
    }
    return longest
};

```

2. **Center-Expand Without Extra Checks (second)**: This has a good balance of readability and efficiency with $O(n^2)$ complexity. Expands around each character or pair and updates `longest` accordingly, making it fast for average cases.
```JS
function longestPalindrome(s) {
    let longest = '';
    function expand(l, r) {
        while (l >= 0 && r < s.length && s[l] === s[r]) {
            if (r - l + 1 > longest.length) longest = s.slice(l, r + 1);
            l--; r++;
        }
    }
    for (let i = 0; i < s.length; i++) {
        expand(i, i);
        expand(i, i + 1);
    }
    return longest;
}
```

### **Best Option**: 
This solution (optimized center-expand with identical-characters check) is best overall, with optimal runtime for diverse cases, and it’s short and efficient.

3. **Optimized Center-Expand With Identical-Characters Check (third)**: This solution checks if all characters are the same, which slightly improves efficiency for homogeneous strings. It then uses the center-expand method, updating `longest` based on comparisons. This solution is the most efficient in terms of average runtime.
```JS
// top runtime
var longestPalindrome = function(s) {
    if (s.length === 1 || s.split('').every(c => c === s[0])) return s;
    
    let longest = '';
    const expand = (l, r) => {
        while (l >= 0 && r < s.length && s[l] === s[r]) l--, r++;
        return s.slice(l + 1, r);
    };

    for (let i = 0; i < s.length; i++) {
        const odd = expand(i, i);
        const even = expand(i, i + 1);
        longest = odd.length > longest.length ? odd : longest;
        longest = even.length > longest.length ? even : longest;
    }
    
    return longest;
};

```


4. **Center-Expand With Start-End Indexing (fourth)**: This is memory-efficient because it uses start and end indices to track the longest palindrome rather than creating substrings repeatedly. It’s fast with $O(n^2)$ complexity and uses minimal memory.
```JS
// top mem
let isPalin =(s, left, right) =>{
    while (left >= 0 && right < s.length && s[left] === s[right]) {
        left--;
        right++;
    }
    return right - left - 1
}
let longestPalindrome =(s)=> {
    let start = 0
    let end = 0;
    for (let i = 0; i < s.length; i++) {
        let len1 = isPalin(s, i, i)
        let len2 = isPalin(s, i, i + 1)
        let len = Math.max(len1, len2)
        if (len > end - start) {
            start = i - Math.floor((len - 1) / 2);
            end = i + Math.floor(len / 2);
        }
    }
    return s.substring(start, end + 1)
};
```

