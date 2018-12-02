# 110 and 111 Balanced Binary Tree and Minimun Depth of Binary Tree

> 这两道题目提醒我们求树的最大高度和树的最小高度不是简单的对称关系，从下面的代码中就可以看出来的，求树的最大高度可以简单使用表达式max(depth(root->left), depth(root->right))，但是求树的最小深度的时候就不是简单的min(depth(root->left), depth(root->right))，要注意如果一边的子树为空是不能加进去作比较的，没有意义。

> 最大深度的代码是：


```C++
int maxDepth(TreeNode* root) {
        if(root == NULL)
        	return 0;
        if(root->left == NULL && root->right == NULL)
        	return 1;
        else{
        	return 1 + max(maxDepth(root->left), maxDepth(root->right));
        }
    }
```



```C++
int minDepth(TreeNode* root) {
        if(root == NULL)
        	return 0;
        if(root->left == NULL && root->right == NULL)
        	return 1;
        else{
        	if(root->left && root->right)
        		return 1 + min(minDepth(root->left), minDepth(root->right));
        	if(root->left && !root->right)
        		return 1 + minDepth(root->left)
        	if(!root->left && root->right)
        		return 1 + minDepth(root->right)
        }
    }
```