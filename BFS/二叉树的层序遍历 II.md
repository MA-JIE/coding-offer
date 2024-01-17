给你二叉树的根节点 root ，返回其节点值 自底向上的层序遍历 。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

``` cpp
#include <queue>
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        if(root == nullptr){
            return {};
        }
        vector<vector<int>> result;
        std::queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            vector<int> level;
            const int size = q.size();
            for(int i=0; i < size; ++i){
                TreeNode* node = q.front();
                q.pop();
                level.push_back(node->val);
                if(node->left != nullptr){
                    q.push(node->left);
                }
                if(node->right != nullptr){
                    q.push(node->right);
                }
            }
            if(!level.empty()){
                result.insert(result.begin(),level);
            }
        }
        return result;
    }
};
```
