### Description:

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).


### Examples (input --> output):

Example 1:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```
Example 2:
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

### Constraints:

```
nums1.length == m
nums2.length == n
0 <= m <= 1000
0 <= n <= 1000
1 <= m + n <= 2000
-106 <= nums1[i], nums2[i] <= 106
```

### Solutions

#### C 

```C
// O(log(min(m, n)))
double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size) {
    if (nums1Size > nums2Size) return findMedianSortedArrays(nums2, nums2Size, nums1, nums1Size);
    int x = nums1Size, y = nums2Size, low = 0, high = x;
    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;
        
        int maxX = (partitionX == 0) ? INT_MIN : nums1[partitionX - 1];
        int minX = (partitionX == x) ? INT_MAX : nums1[partitionX];
        int maxY = (partitionY == 0) ? INT_MIN : nums2[partitionY - 1];
        int minY = (partitionY == y) ? INT_MAX : nums2[partitionY];
        
        if (maxX <= minY && maxY <= minX) {
            if ((x + y) % 2 == 0) return ((double)fmax(maxX, maxY) + fmin(minX, minY)) / 2;
            else return (double)fmax(maxX, maxY);
        } else if (maxX > minY) high = partitionX - 1;
        else low = partitionX + 1;
    }
    return -1;
}
```

#### JS

```JS
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    let temp = nums1.concat(nums2).sort((a,b)=> a-b)
    let even = temp.length % 2 == 0 
    let mid =  even? [(temp.length/2)-1,temp.length/2]: Math.floor((temp.length/2))
    if(even){
        return (temp[mid[0]]+temp[mid[1]])/2
    }
    return temp[mid]
};
```

```JS
//  O((m+n) log(m+n))
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    let a=nums1.concat(nums2).sort((a,b)=>(a-b))
    let middle=Math.floor(a.length/2)
    if(a.length%2==1){
        return a[middle]
    }
        return (a[middle-1]+a[middle])/2     
};
```
