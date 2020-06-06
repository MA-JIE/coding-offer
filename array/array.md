# 1.盛最多水的容器
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。
找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。<br>
示例:<br>
输入：[1,8,6,2,5,4,8,3,7]<br>
输出：49
* 思路:双指针的思路,第一次看到这个题很难去想到双指针的思路.数组两端同时开始便利,并记录面积的最大值,移动的原则:谁的值小,谁就移动.<br>
``` cpp
class Solution
{
public:
    int maxArea(vector<int> &height)
    {
        if (height.size() < 2)
        {
            return 0;
        }
        int ans = 0;
        //取两端指针
        auto left = height.begin();
        auto right = height.end() - 1;
        while (left < right)
        {
            int area = (right - left) * std::min(*left, *right);
            ans = std::max(area, ans);
            //判断应该移动哪边的指针
            (*left > *right) ? right-- : left++;
        }
        return ans;
    }
};
```

# 2.三数之和
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。<br>
注意：答案中不可以包含重复的三元组。<br>
示例:<br>
给定数组 nums = [-1, 0, 1, 2, -1, -4]，<br>

满足要求的三元组集合为：<br>
[                    <br>
  [-1, 0, 1],         <br>
  [-1, -1, 2]         <br>
]                     <br>
``` cpp

```
