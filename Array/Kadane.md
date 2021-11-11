# Kadane

Kadane's algorithm is used to find the maximum sum subarray(*contiguous*) from a given array. It's a DP algorithm.

* The algorithm maintains two variables maxNow and maxSoFar, maxNow keeps track of the max in the current cell and the other keeps track of the max of the overall array upto current cell.
* maxNow chooses the max of the current array value and the sum of (current array value + maxNow upto the previous cell)
* maxSoFar chooses the max of current maxNow and maxSoFar upto the last cell
* maxNow determines the begining index of the contiguous subarray and maxSoFar determines the ending index

There are various versions of the algorithm, the below shown can manage all cases (i.e. -ve and +ve inputs).

## Algorithm

```cpp
// Time: O(N)
// Space: O(1)
int kadane(vector<int> &Array) {
    int maxNow = Array[0], maxSoFar = Array[0];
    for (int i=1;i<Array.size();i++){
	maxNow = max(Array[i],maxNow+Array[i]);
	maxSoFar = max(maxSoFar,maxNow);
    }
    return maxSoFar;
}
```

## Problems

* [363. Max Sum of Rectangle No Larger Than K (Hard)](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/solution/)
