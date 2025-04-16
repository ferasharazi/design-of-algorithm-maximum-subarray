
## Maximum Subarray Problem using Divide and Conquer  

## Description  
The Maximum Subarray problem is a classic challenge in computer science. Given a one-dimensional array of integers (with both positive and negative values), the task is to find the contiguous subarray with the largest sum.  

### Key Concepts  
- **Contiguous Subsequence**: A sequence of consecutive elements in the array (e.g., `[3, -2, 5]` in `[3, -2, 5, -1]`).  
- **Highest Possible Sum**: The largest sum of any contiguous subarray. This could be a single element (if all are negative) or the entire array (if all are non-negative).  

### Example  
Array: `[-2, -3, 4, -1, -2, 1, 5, -3]`  
Maximum Subarray: `[4, -1, -2, 1, 5]` with sum **7**.  

---

## Divide and Conquer Strategy  
1. **Divide**: Split the array `A[low...high]` into two subarrays at midpoint `mid`.  
2. **Conquer**:  
   - Find the maximum subarray in the left half `A[low...mid]`.  
   - Find the maximum subarray in the right half `A[mid+1...high]`.  
   - Find the maximum subarray crossing the midpoint.  
3. **Combine**: Return the maximum sum from the three results.  

![Figure 1: Subarray Locations](Figure1.png)  
*Possible locations of subarrays: entirely in left/right half or crossing the midpoint.*  

![Figure 2: Crossing Subarray Example](Figure2.png)  
*A subarray crossing the midpoint spans from `A[i..mid]` to `A[mid+1..j]`.*  

### Example Execution  
For array `[-2, -5, 6, -2, -6, 1, 5, -6]`:  
![Step-by-Step Solution](Figure3.png)  
**Result**: Maximum subarray is `[1, 5]` with sum **6**.  

---

### Pseudocode for `MaxCrossingSubarray`  
```python  
def MaxCrossingSubarray(A, low, mid, high):  
    # Find max subarray in left half  
    left_sum = -inf  
    sum = 0  
    max_left = mid  
    for i in range(mid, low-1, -1):  
        sum += A[i]  
        if sum > left_sum:  
            left_sum = sum  
            max_left = i  

    # Find max subarray in right half  
    right_sum = -inf  
    sum = 0  
    max_right = mid+1  
    for j in range(mid+1, high+1):  
        sum += A[j]  
        if sum > right_sum:  
            right_sum = sum  
            max_right = j  

    return (max_left, max_right, left_sum + right_sum)