# 1.最长回文子串
回文串：轴对称的字符串。<br>
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。<br>
示例：<br>
输入: "babad" <br>
输出: "bab"  <br>
注意: "aba" 也是一个有效答案。<br>
输入: "cbbd" <br>
输出: "bb" <br>
思路：动态规划的思想，因为dp是一个非常重要的思想，所以列出dp的解法。<br>
对于最初的子问题，含有一个字符时，本身就是回文串；含有两个字符时，只有相等才为回文串；大于两个字符时，保证首尾相同，还要保证包含的子字符串相同才为回文串....如此迭代，不断更新回文串的长度。这里认为最难想到的是：声明一个dp的二维(n,n)数组,行代表字符串的首，列代表字符串的尾，从字符串长度为0开始不断遍历。
``` cpp
class Solution
{
public:
    string longestPalindrome(string s)
    {
        int n = s.size();
        //声明一个二维数组
        vector<vector<int>> dp(n, vector<int>(n));
        string ans;
        for (int l = 0; l < n; l++)
        {
            for (int i = 0; i + l < n; i++)
            {
                //i代表子字符串首的位置，j代表子字符串尾的位置
                int j = i + l;
                //字符串长度为1时
                if (l == 0)
                {
                    dp[i][j] = 1;
                }
                //字符串长度为2时
                else if (l == 1)
                {
                    dp[i][j] = (s[i] == s[j]);
                }
                else
                {
                    //首尾相同&&子字符串也为回文串
                    dp[i][j] = (s[i] == s[j] && dp[i + 1][j - 1]);
                }
                //取处最长的回文串
                if (dp[i][j] && l + 1 > ans.size())
                {
                    ans = s.substr(i, l + 1);
                }
            }
        }
        return ans;
    }
};

```

# 2.Z 字形变换
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。<br>
比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：<br>
L   C   I   R <br>
E T O E S I I G <br>
E   D   H   N  <br>
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。<br>
思路：这道题最基本的思路是建立二维数组，并寻找其排列的规律。<br>
但是还可以按行排序: 将每行的字符收集到一起，最后在整体结合输出。当处在第0行时，按行向下遍历，当处在最后一行时，按行向上遍历，如此反复。<br>

``` cpp
class Solution
{
public:
    string convert(string s, int numRows)
    {
        if (numRows == 1)
        {
            return s;
        }
        //每个索引代表一行字符串
        vector<string> rows(min(numRows, int(s.size())));
        //定义bool值，决定是不是要向下换行
        bool goingdown = false;
        //从0行开始
        int currentRow = 0;
        string result;
        for (auto val : s)
        {
            rows[currentRow] += val;
            //如果当前行在第一行或者最后一行，goingdown取反
            if (currentRow == 0 || currentRow == numRows - 1)
            {
                goingdown = !goingdown;
            }
            currentRow += goingdown ? 1 : -1;
        }
        for (auto val : rows)
        {
            result += val;
        }
        return result;
    }
};
```
