# 1. Two Sum

## 1st

まずは愚直に全探索をしてみた。

N: numsの要素数
- 時間計算量: $O(N^2)$
- 空間計算量: $O(1)$

`nums.length()`と書いたらエラー出たので[参照先](https://en.cppreference.com/w/cpp/container/vector)で調べたら.size()が正しいとわかった。.length()が使えるのは`std::string`だった。

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        for (int i = 0; i < nums.size() - 1; i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    ans.push_back(i);
                    ans.push_back(j);
                    break ;
                }
            }
        }
        return ans;
    }
};
```

## 2nd

ハッシュマップを使うことで2重ループせずに探索できる。

最大でN-1個分の要素をハッシュマップに保存するので計算量は以下の通り

N: numsの要素数
- 時間計算量: $O(N)$
- 空間計算量: $O(N)$

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;

        for (int i = 0; i < nums.size(); i++) {
            if (mp.count(target - nums[i]) > 0) {
                return {mp[target - nums[i]], i};
            }
            mp[nums[i]] = i;
        }
        return {};
    }
};
```

## 3rd

時間: 40s

N: numsの要素数
- 時間計算量: $O(N)$
- 空間計算量: $O(N)$

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> numsMap;

        for(int i = 0; i < nums.size(); i++) {
            if (numsMap.count(target - nums[i]) > 0) {
                return {numsMap[target - nums[i]], i};
            }
            numsMap[nums[i]] = i;
        }
        return {};
    }
};
```

## 4rd

時間: 1分30秒

レビューを受けて、`unordered_map` のデータの変数名を修正しました。

nums[i]をkey, iをvalueとして持つので、num_to_indexです

for文を終えた後は要件を満たしていないnumsかtargetが渡されてきたことになるので、
errorメッセージを出力して空配列を出力するようにしました。

この問題からユースケースを思い浮かべることは難しかったです。

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> num_to_index;

        for(int i = 0; i < nums.size(); i++) {
            if (num_to_index.contains(target - nums[i])) {
                return {num_to_index[target - nums[i]], i};
            }
            num_to_index[nums[i]] = i;
        }
        cout << "input value error" << endl;
        return {};
    }
};
```
