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