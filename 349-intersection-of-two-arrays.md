- nums1をunordered_setに登録して重複をなくしていく
- 重複のなくなったnums1に対してnums2の数値と同じものを探す
- 同じものがあったときにansにpush_backしていく

数値は0~1000という制約があったので、1001個の要素を持つ配列を用意し
ans.push_backをするときにその数値をindexとして値を1にすることで重複をチェック
ただこの方法だと数値の範囲が広がった時にスケールしづらい書き方なので、setを使ったほうがいいのかな？

nums1.lengthをN, nums2.lengthをKとすると

時間計算量O(N+K)

空間計算量O(N)

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        int exist_nums2[1001] = {};
        vector<int> ans;
        unordered_set<int> nums1_set;
        for(int i = 0; i < nums1.size(); i++) {
            nums1_set.insert(nums1[i]);
        }
        for(int i = 0; i < nums2.size(); i++) {
            if (nums1_set.contains(nums2[i]) && exist_nums2[nums2[i]] != 1) {
                ans.push_back(nums2[i]);
                exist_nums2[nums2[i]] = 1;
            }
        }
        return ans;
    }
};
```
