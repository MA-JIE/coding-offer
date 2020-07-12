# Pow(x, n)
实现 pow(x, n) ，即计算 x 的 n 次幂函数。<br>
示例 1: <br>
输入: 2.00000, 10 <br>
输出: 1024.00000  <br>
示例 2: <br>
输入: 2.10000, 3 <br>
输出: 9.26100  <br>
示例 3: <br>
输入: 2.00000, -2 <br>
输出: 0.25000  <br>
解释: 2-2 = 1/22 = 1/4 = 0.25 <br>
思路: https://leetcode-cn.com/problems/powx-n/solution/powx-n-by-leetcode-solution/ <br>
n 为奇数时, 幂数加一 , 注意边界条件的判定<br>
``` cpp
class Solution
{
public:
    //这里的n >= 0
    double quickmul(double x, int n)
    {
        double res = 1.0;
        double x_contribute = x;
        while (n > 0)
        {
            //如果n是奇数,进行幂+1的操作
            if (n % 2 == 1)
            {
                res *= x_contribute;
            }
            x_contribute *= x_contribute;
            n = n / 2;
        }
        return res;
    }
    double myPow(double x, int n)
    {
        if (x == 1.0)
        {
            return 1.0;
        }
        if (n == INT32_MIN && fabs(x) != 1.0)
        {
            return 0.0;
        }
        long long N = n;
        return N >= 0 ? quickmul(x, N) : 1.0 / quickmul(x, -N);
    }
};

```
