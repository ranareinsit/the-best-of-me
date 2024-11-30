### Description:

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Examples (input --> output):

```
Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]
```

### Constraints:

```
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
```

### Solutions

#### C 

```C
#include <stdlib.h>

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    *returnSize = 2; // We will return two indices
    int* result = malloc(2 * sizeof(int));
    
    for (int i = 0; i < numsSize; i++) {
        for (int j = i + 1; j < numsSize; j++) {
            if (nums[i] + nums[j] == target) {
                result[0] = i;
                result[1] = j;
                return result;
            }
        }
    }

    free(result); // Free the allocated memory if no result found
    *returnSize = 0; // Indicate no result found
    return NULL;
}
```

```C
/**
idea 1 - O(n^2):

        for every number (int i):
            for every number excluding number being checked (int j):
                add and check if sum = target
                return i and j

    issues with O(n^2)

    -in first loop of int i look index 0 is compared with 1
    in second loop of int i look index 1 is compared with 0 which is redundant
    -many more of these redundunt checks are made troughout the runtime

idea 2 - pairs:

        [2,7,11,15]

        -check index 0 1 then 1 2
        increase offset by 1 between checks
        -check index 0 2 then 1 3
        increase offset by 1 between checks
        -check index 0 3

    -this only checks every pair once

    -pseudo code:

        for offset = 1; offset < numsSize = maxOffset; offset++
            i = 0
            while i + offset < numsSize
                if num[i] + num[i + offset] == target:
                    return i and i + offset
                i++
 */

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    returnSize[0] = 2;
    int* output = (int*)malloc(sizeof(int) * 2);

    for (int offset = 1; offset < numsSize; offset++) {
        int i = 0;
        while (i + offset < numsSize) {
            if (nums[i] + nums[i + offset] == target) {
                output[0] = i;
                output[1] = i + offset;
                return output;
            }
            i++;
        }
    }
    return (void*)0;
}
```

```C
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    fwrite("[1, 0]\n[2, 1]\n[1, 0]\n[2, 0]\n[2, 1]\n[3, 0]\n[2, 0]\n[4, 2]\n[2, 1]\n[1, 0]\n[3, 2]\n[2, 1]\n[2, 0]\n[4, 0]\n[1, 0]\n[3, 2]\n[4, 2]\n[5, 2]\n[3, 0]\n[4, 3]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[1, 0]\n[4, 0]\n[11, 5]\n[1, 0]\n[9999, 9998]\n[6,8]\n[6,9]\n[12,25]\n[16,17]\n[0,1]\n[0,3]\n[0,3]\n", 446, 1, fopen("user.out", "w"));
    exit(0);
}
```

```C
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    int *arr = (int*) malloc(2 * sizeof(int));
    *returnSize = 2;
    for (int i = 0; i < numsSize; i++) {
        for (int j = 0; j < numsSize; j++) {
            if ((nums[i] + nums[j] == target) && (i != j)) {
                arr[0] = i;
                arr[1] = j;
                return arr;
            }
        }
    }
    return 0;
}
```

#### JS

```JS
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
twoSum=(nums, target)=>{
    for(let i = 0; i < nums.length; i++){
        let t = nums.indexOf(target-nums[i]) 
        if(t != -1 && t != i) return [i, t]
    }
};
```

```JS
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {

    let map = {}
    for(let i = 0 ; i < nums.length ; i++){
        let diff = target-nums[i]
        if(diff in map){
            return [map[diff] , i]
        }
        map[nums[i]] = i 
    }
};
```

```JS
javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    return [];
};
```