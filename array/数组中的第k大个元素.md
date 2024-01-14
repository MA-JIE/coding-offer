给定整数数组 nums 和整数 k，请返回数组中第 k 个最大的元素。

请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

你必须设计并实现时间复杂度为 O(n) 的算法解决此问题。


``` cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int left = 0;
        int right = nums.size() - 1;
        while (true) {
            int pos = partition(nums, left, right);
            if (pos == k - 1) {
                return nums[pos];
            }
            if (pos > k - 1) {
                right = pos - 1;
            } else {
                left = pos + 1;
            }
        }
    }
    //寻找第k大个元素
    int partition(vector<int>& nums, int left, int right) {
        int pivot = nums[left];
        int l = left + 1;
        int r = right;
        while (l <= r) {
            if (nums[l] < pivot && nums[r] > pivot) {
                swap(nums[l++], nums[r--]);
            }
            if (nums[l] >= pivot) {
                l++;
            }
            if (nums[r] <= pivot) {
                r--;
            }
        }
        swap(nums[left], nums[r]);
        return r;
    }
   //寻找第k小个元素
    int partition(vector<int>& nums, int left, int right) {
        int pivot = nums[left], l = left + 1, r = right;
        while (l <= r) {
            if (nums[l] > pivot && nums[r] < pivot) {
                swap(nums[l++], nums[r--]);
            }
            if (nums[l] <= pivot) {
                l++;
            }
            if (nums[r] >= pivot) {
                r--;
            }
        }
        swap(nums[left], nums[r]);
        return r;
    }
};

```
