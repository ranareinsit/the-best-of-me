### Description:




### Examples (input --> output):

```

```

### Constraints:

```

```

### Solutions

#### C 

```C
#include <string.h>

int lengthOfLongestSubstring(char* s) {
    int maxLen = 0;
    int start = 0;
    int map[128] = {0};  // ASCII map to store the last occurrence of each character
    int n = strlen(s);   // Length of the input string
    
    for (int end = 0; end < n; end++) {
        char current = s[end];
        
        if (map[current] > start) {
            start = map[current];  // Update start to skip the previous occurrence
        }
        
        map[current] = end + 1;  // Store the current index (shifted by 1 to handle zero-index)
        
        int currentLength = end - start + 1;
        if (currentLength > maxLen) {
            maxLen = currentLength;  // Update the max length
        }
    }
    
    return maxLen;
}
```

```C
int lengthOfLongestSubstring(char* s) {
    int longestSubString = 0;
    int lastLongestSubString = 0;
    for ( int i = 0; s[i] != '\0'; i++ ) {
        if ( lastLongestSubString == 0 ) {
            lastLongestSubString = 1;
        }
        for ( int j = i + 1; s[j] != '\0'; j++ ) {
            if ( s[i] == s[j] ) {
                longestSubString = j - i;
                break;
            } else {
                longestSubString = j - i + 1;
            }
        }

        for ( int k = i + 1; k < (i + longestSubString); k++ ) {
            for ( int l = k + 1; l < (i + longestSubString); l++ ) {
                if ( s[k] == s[l] ) {
                    longestSubString = l - i;
                    break;
                }
            }
        }

        if ( longestSubString > lastLongestSubString ) {
            lastLongestSubString = longestSubString;
        }
    }

    return lastLongestSubString;
}
```

#### JS

```JS
function lengthOfLongestSubstring(s) { // O(n)
    let maxLen = 0;
    let start = 0;
    let map = new Map();

    for (let end = 0; end < s.length; end++) {
        if (map.has(s[end])) {
            start = Math.max(map.get(s[end]) + 1, start);
        }
        map.set(s[end], end);
        maxLen = Math.max(maxLen, end - start + 1);
    }

    return maxLen;
}
```

```JS
const isUnic = a => new Set(a).size === a.length;

function lengthOfLongestSubstring(s) { //  O(n²)
    let count = 0;
    for (let i = 0; i < s.length; i++) {
        for (let j = i + 1; j <= s.length; j++) {
            let substring = s.slice(i, j);
            if (isUnic([...substring])) {
                count = Math.max(count, substring.length);
            } else {
                break;
            }
        }
    }
    return count;
}

```