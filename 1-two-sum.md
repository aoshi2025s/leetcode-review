# 1. Two Sum

## 1st

まずは愚直に全探索をしてみた。

N: numsの要素数
- 時間計算量: $O(N^2)$
- 空間計算量: $O(N)$

計算量の見積もりの仕方はよくわかっていないです。numsの要素分のメモリが必要だと考えたので空間計算量はO(N)にしましたが、見積もるのは追加のメモリ、つまりansの要素数だけでいいのでしょうか？

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