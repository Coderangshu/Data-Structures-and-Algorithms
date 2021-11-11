# Interleaving Placement

Rearranging the elements of an array in such a way that no two adjacent elements are equal.

## Algorithm
```cpp
// Time: O(N)
// Space: O(1)
void interleavingPlacement(int arr[], int n) {
    unordered_map<int,int> frequencyDictionary;
    for (int i = 0; i < n; i++) frequencyDictionary[arr[i]]++;
    priority_queue<pair<int,int>,vector<pair<int,int>>> maxHeap;
    for(auto e:frequencyDictionary) maxHeap.push({e.second,e.first});
    vector<int> ans;
    while(maxHeap.size()>1){
        auto [freq,val]=maxHeap.top();
        maxHeap.pop();
        auto [freq2,val2]=maxHeap.top();
        maxHeap.pop();
        ans.push_back(val);
        ans.push_back(val2);
        if(freq>1) maxHeap.push({freq-1,val});
        if(freq2>1) maxHeap.push({freq2-1,val2});
    }
    if(maxHeap.size()==1) ans.push_back(maxHeap.top().second);
    return ans;
}
```

## Problems

* [767. Reorganize String (Medium)](https://leetcode.com/problems/reorganize-string/)
* [1054. Distant Barcodes (Medium)](https://leetcode.com/problems/distant-barcodes/)