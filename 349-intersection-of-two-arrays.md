とりあえずで思いついたのは、片方をハッシュマップやセットなどのデータ構造に入れて、重複を無くす
その後もう片方の要素を一つずつ見て行って、先ほど入れたデータ構造に入っていたら出力する
その際も重複チェックをするという方針
今ある知識だとunordered_mapくらいしかないので一旦これを使うことに
keyに対するvalueは何の意味もないという無駄などがあると思いつつも一旦書き上げることを優先

時間計算量O(N)
空間計算量O(N)

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> mp;
        unordered_map<int, int> mp2;
        vector<int> ans;
        for (int i = 0; i < nums1.size(); i++) {
            mp[nums1[i]] = 1;
        }
        for (int i = 0; i < nums2.size(); i++) {
            if (mp.contains(nums2[i]) && (mp2.contains(nums2[i]) == false)) {
                ans.push_back(nums2[i]);
                mp2[nums2[i]] = 1;
            } else {
                mp2[nums2[i]] = 1;
            }
        }
        return ans;
    }
};
```
