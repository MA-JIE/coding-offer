给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径

``` cpp
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        vector<vector<int>> result;
        vector<int> single_path;
        isPath(root, targetSum, &single_path,&result);
        return result;
    }

    void isPath(TreeNode* root, int targetSum, vector<int>* single_path, vector<vector<int>>* record) const {
        if(root == nullptr){
            return;
        }
        single_path->push_back(root->val);
        bool is_leaf_node = root->left == nullptr && root->right == nullptr;
        if(is_leaf_node && targetSum - root->val == 0 ){
          record->push_back(*single_path);
        }
        isPath(root->left, targetSum - root->val, single_path,record);
        isPath(root->right, targetSum - root->val, single_path,record);
        single_path->pop_back();
    }
};
```
