# 1.电话号码的字母组合
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。<br>
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。<br>
示例：<br>
输入："23" <br>
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].<br>

``` cpp
class Solution
{
public:
    map<char, string> M = {{'2', "abc"},
                           {'3', "def"},
                           {'4', "ghi"},
                           {'5', "jkl"},
                           {'6', "mno"},
                           {'7', "pqrs"},
                           {'8', "tuv"},
                           {'9', "wxyz"}};
    vector<string> ans;
    string current;
    void DFS(int index, string digits)
    {
        //递归基，当index等于输入长度时，ans进行pushback,返回
        if (index == digits.size())
        {
            ans.emplace_back(current);
            return;
        }

        for (int i = 0; i < M[digits[index]].size(); i++)
        {
            current.push_back(M[digits[index]][i]);
            DFS(index + 1, digits);
            current.pop_back();
        }
    }
    vector<string> letterCombinations(string digits)
    {
        if (digits.size() == 0)
        {
            return ans;
        }
        DFS(0, digits);
        return ans;
    }
};
```
# 2.组合总和
给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。<br>
candidates 中的数字可以无限制重复被选取。<br>
说明：<br>
所有数字（包括 target）都是正整数。<br>
解集不能包含重复的组合。<br>
示例：<br>
输入: candidates = [2,3,6,7], target = 7,
所求解集为:<br>
[ <br>
  [7], <br>
  [2,2,3] <br>
] <br>
输入: candidates = [2,3,5], target = 8,
所求解集为:<br>
[ <br>
  [2,2,2,2],<br>
  [2,3,3],<br>
  [3,5] <br>
]<br>

```cpp
class Solution
{
private:
    vector<int> candidates;
    //输出结果
    vector<vector<int>> res;
    //当前路径
    vector<int> path;
    //start代表index
    void DFS(int start, int target)
    {
        //递归基，如果为0，说明该条路径满足条件，加入result中，并返回
        if (target == 0)
        {
            res.emplace_back(path);
            return;
        }
        //从start开始，避免了重复出现的数组,判定条件中若target小于对应元素，返回
        for (int i = start; i < candidates.size() && target - candidates[i] >= 0; i++)
        {
            //现将元素加入path
            path.emplace_back(candidates[i]);
            //递归实现
            DFS(i, target - candidates[i]);
            //将元素弹出，进入下次迭代
            path.pop_back();
        }
    }

public:
    vector<vector<int>> combinationSum(vector<int> &candidates, int target)
    {
        //先进行排序操作为了提高搜索速度
        std::sort(candidates.begin(), candidates.end());
        this->candidates = candidates;
        DFS(0, target);
        return res;
    }
};
```
# 3.组合总和 II
给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。<br>
candidates 中的每个数字在每个组合中只能使用一次。<br>
说明：<br>
所有数字（包括目标数）都是正整数。<br>
解集不能包含重复的组合。 <br>
示例：<br>
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:<br>
[<br>
  [1, 7],<br>
  [1, 2, 5],<br>
  [2, 6],<br>
  [1, 1, 6]<br>
]<br>
思路：该题和上一题的思路差不多，不过需要注意的是每次迭代一遍后，都要判断此时的值是否与相邻值相同，若相同，则舍去，不然会造成重复数组的出现。<br>
```cpp
class Solution
{
private:
    vector<int> candidates;
    vector<vector<int>> res;
    vector<int> path;
    void DFS(int start, int target)
    {
        if (target == 0)
        {
            res.emplace_back(path);
            return;
        }
        for (int i = start; i < candidates.size() && target - candidates[i] >= 0; ++i)
        {
            //i > start代表着进入下一次迭代
            if (i > start && candidates[i] == candidates[i - 1])
            {
                continue;
            }
            path.emplace_back(candidates[i]);
            DFS(i + 1, target - candidates[i]);
            path.pop_back();
        }
    }

public:
    vector<vector<int>> combinationSum2(vector<int> &candidates, int target)
    {
        std::sort(candidates.begin(), candidates.end());
        this->candidates = candidates;
        DFS(0, target);
        return res;
    }
};
```
