# Count Inversions In An Array

In array `A`, two elements `A[i]` and `A[j]` form an inversion if `A[i] > A[j]` and `i < j`

_The count of inversion_ of an array indicates how far the array is from sorted. If the array is already sorted, its inversion count is 0. If the array is sorted in the reverse order then its inversion count is the maximum.

### Brute force

Brute force method is trivial -- for each number, count how many number to its right is smaller than it. The time complexit is `O(N^2)` and space complexity is `O(1)`.

### Merge Sort \(Divide and Conquer\)

During the merge, if we need to select a number `x` from the right part, we can add the inversion count by the count of remaining items in the left part, because they must be all greater than `x`.

For example, assume we want to merge `[1,3]` and `[0,2]`.

* we need to first select the `0` and there are `2` numbers left in the left part, we add the count by `2`.
* select `1` from the left part, leave the count unchanged.
* select `2` from the right part, add the count by `1` because there is only one `3` left in the left part.
* select `3` from the left part, leave the count unchanged.

So in total there are `2 + 1 = 3` inversions.

```cpp
// Time: O(NlogN)
// Space: O(N)
long long merger(long long arr[], long long l, long long m, long long r){
    long long n1 = m-l, n2 = r-m+1, c = 0;
    long long la[n1], ra[n2];
    for(long long i=0;i<n1;i++) la[i] = arr[l+i];
    for(long long i=0;i<n2;i++) ra[i] = arr[m+i];
    long long i = 0, j = 0, k = l;
    while(i<n1 and j<n2){
        if(la[i]>ra[j]){
            arr[k++] = ra[j++];
            c += m-(i+l);
        }
        else arr[k++] = la[i++];
    }
    while(i<n1) arr[k++] = la[i++];
    while(j<n2) arr[k++] = ra[j++];
    return c;
}
    
long long partitioner(long long arr[], long long l, long long r){
    long long c = 0;
    if(l<r){
        long long m  = (r+l)>>1;
        c += partitioner(arr,l,m);
        c += partitioner(arr,m+1,r);
        c += merger(arr,l,m+1,r);
    }
    return c;
}
        
long long int inversionCount(long long arr[], long long N){
    long long ans = partitioner(arr,0,N-1);
    return ans;
}
```

