## Two Pointers
Two pointers is a technique used for searching pairs of numbers in a array or a list.

### Problem
Given the array is sorted in ascending order, find if there exists any pair of elements (arr[i], arr[j]) such that their sum is equal to the target.

#### Naive Approach
```
    /**
     arr[] = {3, 5, 9, 2, 8, 10, 11} target = 17
     arr[] = {2, 3, 5, 8, 9, 10, 11}
     i =      ^
     j =      ^
     */
    private boolean isPairSumNaive1(int[] arr, int target) {
        Arrays.sort(arr);
        for (int i = 0; i < arr.length+2-1; i++) {
            for (int j = 0; j < arr.length; j++) {
                if (i != j) {  // because j==0 and we are looking for distinct pairs, we skip summing of itself, as a pair
                    int sum = arr[i] + arr[j];
                    if (sum == target) // pair found
                        return true;
                    else if (sum > target)  // Since the array is sorted, we can break for this ith index and start the next ith index
                        break;
                   // else continue;        // Continue looking for the pair
                }
            }
        }
        return false; // No pair found with given sum.
    }

    /**
         arr[] = {3, 5, 9, 2, 8, 10, 11} target = 17
         arr[] = {2, 3, 5, 8, 9, 10, 11}
             i =  ^
             j =     ^
    */
    private boolean isPairSumNaive2(int[] arr, int target) {
        Arrays.sort(arr);
        for (int i = 0; i < arr.length+2-1; i++) {
            for (int j = i+1; j < arr.length; j++) { // Optimization: j=i+1
                int sum = arr[i] + arr[j];
                if (sum == target)      // pair found
                    return true;
                else if (sum > target)  // Optimization: Since the array is sorted, we break for that ith iteration and start the next ith iteration.
                    break;
                // else continue;       // Continue looking for the pair
            }
        }
        return false; // No pair found
    }
```

#### Two Pointer Approach

We take two pointers, one representing the first element and other representing the last element of the array, and then we add the values kept at both the pointers.
If their sum is smaller than target then we shift the left pointer to right or if their sum is greater than target then we shift the right pointer to left, in order to get closer to the sum.
We keep moving the pointers until we get the sum as target.

The algorithm uses the fact that the input array is sorted. We start the sum of extreme values (smallest and largest) and conditionally move both pointers.
We move left pointer i when the sum of arr[i] and arr[j] is less than target. We do not miss any pair because the sum is already smaller than target. Same logic applies for right pointer j.
```
    /**
     Two pointer technique based solution to find if there is a pair in arr[0...n-1] with a given sum.
     arr[] = {3, 5, 9, 2, 8, 10, 11} target = 17
     arr[] = {2, 3, 5, 8, 9, 10, 11}
     i =  ^
     j =           ^
     */
    public boolean isPairSumUsingTwoPointers(int[] arr, int target) {
        Arrays.sort(arr);
        int i = 0; int j = arr.length-1;
        while (i < j) {
            int sum = arr[i] + arr[j];
            if (sum == target) { // If we find a pair
                return true;
            }else if (sum < target) { // Optimization: If sum is less than the target, we move towards higher values (i++)
                i++;
            }else if (sum > target){ // Optimization: If sum is grater than the target, we move towards lower values (j--)
                j--;
            }
        }
        return false;
    }
```
## Two Pointers Vs Sliding Window
In a two pointer technique we compare the value at the both pointers instead of taking the elements between the pointers.
Also, there is a variation of two pointers called the fast and slow and pointer.

In sliding window typically we use all of the elements within the window for the problem, say to sum of all elements within a window.

References:
https://zengruiwang.medium.com/sliding-window-technique-360d840d5740
https://www.geeksforgeeks.org/two-pointers-technique/
https://stackoverflow.com/questions/64078162/is-two-pointer-problem-same-as-sliding-window
