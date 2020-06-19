# Z 字形变换
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。<br>
比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：<br>
L   C   I   R <br>
E T O E S I I G <br>
E   D   H   N <br>
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。<br>
示例：<br>
输入: s = "LEETCODEISHIRING", numRows = 3 <br>
输出: "LCIRETOESIIGEDHN" <br>
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
