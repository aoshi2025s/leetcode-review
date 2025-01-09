# Step 1

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
# Step 2

他の方の解法や書き方を参考にした

- 解法1
nums1とnums2それぞれで重複チェックをしなくても、nums1の重複削除したデータ構造を持っておいて、nums2と一致するか確かめた後にその要素を削除していけば良いことがわかった</br>
記法として `unordered_set<int> unique_nums1(nums1.begin(), nums1.end());` や `for (int num: nums1)` のような書き方を知った

- 解法2
`set_intersection`というものがある</br>https://cpprefjp.github.io/reference/algorithm/set_intersection.html</br>
他の方が使っていた`back_inserter`が全然知らない概念のものだったので理解が難しかった</br>
また、ソート済みのものを与える必要があるので、`unordered_set`はここでは使えなかった

- 解法3
nums1とnums2をソートさせるという解法があるとわかった</br>
例えばnums1またはnums2の要素数が莫大でメモリ上に乗らない場合でも、ソート済みであれば要素を一つずつ取ってきて一致するかどうかを確かめられる

## 解法1
nums1のサイズをN, nums2のサイズをKとするとき
- 時間計算量: O(N + K)
- 空間計算量: O(N + K)
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> unique_nums1(nums1.begin(), nums1.end());
        vector<int> intersected_nums;

        for (int num: nums2) {
            if (unique_nums1.contains(num)) {
                intersected_nums.push_back(num);
                unique_nums1.erase(num);
            }
        }
        return intersected_nums;
    }
};
```

## 解法2
nums1のサイズをN, nums2のサイズをKとするとき</br>
- 時間計算量: O(N + K)
- 空間計算量: O(N + K)
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        set<int> unique_nums1(nums1.begin(), nums1.end());
        set<int> unique_nums2(nums2.begin(), nums2.end());
        vector<int> intersected_nums;

        set_intersection(
            unique_nums1.begin(), unique_nums1.end(),
            unique_nums2.begin(), unique_nums2.end(),
            inserter(intersected_nums, intersected_nums.end())
        );
        return intersected_nums;
    }
};
```

## 解法3
nums1のサイズをN, nums2のサイズをKとするとき</br>
- 時間計算量: O(min(N, K) + Nlog(N) + Klong(K))
- 空間計算量: O(N + K)
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        vector<int> intersected_nums;

        int i = 0;
        int j = 0;
        while (i < nums1.size() && j < nums2.size()) {
            if (nums1[i] < nums2[j]) {
                i++;
                continue;
            }
            if (nums1[i] > nums2[j]) {
                j++;
                continue;
            }
            int common = nums1[i];
            intersected_nums.push_back(common);
            while (i < nums1.size() && nums1[i] == common) {
                i++;
            }
            while (j < nums2.size() && nums2[j] == common) {
                j++;
            }
        }
        return intersected_nums;
    }
};
```

# step 3
nums1のサイズをN, nums2のサイズをKとするとき
- 時間計算量: O(N + K)
- 空間計算量: O(N + K)
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> unique_nums1(nums1.begin(), nums1.end());
        vector<int> intersected_nums;

        for (int num: nums2) {
            if (unique_nums1.contains(num)) {
                intersected_nums.push_back(num);
                unique_nums1.erase(num);
            }
        }
        return intersected_nums;
    }
};
```
