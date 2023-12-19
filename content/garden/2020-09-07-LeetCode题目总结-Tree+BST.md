---
title: LeetCode题目总结-Tree+BST
date: 2020-09-07 21:13:19
categories: 
- LeetCode
tags:
- C++
- 算法
- ch
---

### 题目94:[二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

---

描述：

给定一个二叉树，返回它的中序 遍历。

示例:

输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？

<!--more-->

[思路一](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/che-di-chi-tou-er-cha-shu-de-qian-zhong-hou-xu-di-/)：

突破点：`递归。`

代码：

```c++
void traversal(TreeNode* cur, vector<int>& vec) {
    if (nullptr == cur) return;
    traversal(cur->left, vec);  // 左
    vec.push_back(cur->val);    // 中
    traversal(cur->right, vec); // 右
}
```

[思路二](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/che-di-chi-tou-er-cha-shu-de-qian-zhong-hou-xu-di-/)：

突破点：`迭代。`

代码：

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> tempStack;
        if (nullptr != root) tempStack.push(root);
        while (!tempStack.empty()) {
            TreeNode* node = tempStack.top();
            if (nullptr != node) {
              	// 将该节点弹出，避免重复操作，下面再将右中左节点添加到栈中
                tempStack.pop(); 
              	// 添加右节点
                if (node->right) tempStack.push(node->right); 
              	// 添加中节点
                tempStack.push(node);
              	// 中节点访问过，但是还没有处理，需要做一下标记。
                tempStack.push(nullptr); 
								// 添加左节点
                if (node->left) tempStack.push(node->left); 
            } else {
              	// 将空节点弹出
                tempStack.pop(); 
              	// 重新取出栈中元素
                node = tempStack.top(); 
                tempStack.pop();
              	// 加入到数组中
                result.push_back(node->val); 
            }
        }
        return result;
    }
};
```

---

### 题目144:[二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

---

描述：

给定一个二叉树，返回它的 前序 遍历。

示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？

[思路一](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/dai-ma-sui-xiang-lu-chi-tou-qian-zhong-hou-xu-de-d/)：

突破点：`递归。`

代码：

```c++
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& vec) {
        if (nullptr == cur) return;
        vec.push_back(cur->val);    // 中
        traversal(cur->left, vec);  // 左
        traversal(cur->right, vec); // 右
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```

[思路二](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/dai-ma-sui-xiang-lu-chi-tou-qian-zhong-hou-xu-de-d/)：

突破点：`迭代。`

代码：

```c++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> tempStack;
        if (nullptr != root) tempStack.push(root);
        while (!tempStack.empty()) {
            TreeNode* node = tempStack.top();
            if (nullptr != node) {
                tempStack.pop();
                if (node->right) tempStack.push(node->right);  // 右
                if (node->left) tempStack.push(node->left);    // 左
                tempStack.push(node);                          // 中
                tempStack.push(NULL);
            } else {
                tempStack.pop();
                node = tempStack.top();
                tempStack.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};
```

---

### 题目145:[二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

---

描述：

给定一个二叉树，返回它的 后序 遍历。

示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？

思路一：

突破点：`递归。`

代码：

```c++
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& vec) {
        if (nullptr == cur) return;
        traversal(cur->left, vec);  // 左
        traversal(cur->right, vec); // 右
        vec.push_back(cur->val);    // 中
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```

[思路二](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/dai-ma-sui-xiang-lu-chi-tou-qian-zhong-hou-xu-de-d/)：

突破点：`迭代。`

代码：

```c++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> tempStack;
        if (nullptr != root) tempStack.push(root);
        while (!tempStack.empty()) {
            TreeNode* node = tempStack.top();
            if (nullptr != node) {
                tempStack.pop();
                tempStack.push(node);                          // 中
                tempStack.push(NULL);

                if (node->right) tempStack.push(node->right);  // 右
                if (node->left) tempStack.push(node->left);    // 左
            } else {
                tempStack.pop();
                node = tempStack.top();
                tempStack.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};
```

---

### 题目112:[路径总和](https://leetcode-cn.com/problems/path-sum/)

---

描述：
给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

**说明:** 叶子节点是指没有子节点的节点。

**示例:** 
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

返回 `true`, 因为存在目标和为 22 的根节点到叶子节点的路径 `5->4->11->2`。

[思路一](https://leetcode-cn.com/problems/path-sum/solution/lu-jing-zong-he-by-leetcode-solution/)：

突破点：`广度优先搜索。`

步骤：

1. 使用广度优先搜索，计算从根节点到当前节点的路径和；
2. 使用两个队列，分别存储要遍历的节点和根节点到这些节点的路径和。

代码：

```c++
class Solution {
public:
    bool hasPathSum(TreeNode *root, int sum) {
        if (nullptr == root) {
            return false;
        }
        queue<TreeNode *> queNode;
        queue<int> queVal;
        queNode.push(root);
        queVal.push(root->val);
        while (!queNode.empty()) {
            TreeNode *now = queNode.front();
            int temp = queVal.front();
            queNode.pop();
            queVal.pop();
            if (nullptr ==now->left && nullptr == now->right) {
                if (temp == sum) return true;
                continue;
            }
            if (nullptr != now->left) {
                queNode.push(now->left);
                queVal.push(now->left->val + temp);
            }
            if (now->right != nullptr) {
                queNode.push(now->right);
                queVal.push(now->right->val + temp);
            }
        }
        return false;
    }
};
```

[思路二](https://leetcode-cn.com/problems/path-sum/solution/lu-jing-zong-he-by-leetcode-solution/)：

突破点：`递归。`

步骤：

1. 问题细化，即为求是否存在从当前节点的子节点到叶子节点的路径，使得路径和为sum-val；
2. 若当前节点为叶子节点，则直接判断sum是否与val相等；
3. 若非叶子节点，需递归进行查询。

代码：

```c++
class Solution {
public:
    bool hasPathSum(TreeNode *root, int sum) {
        if (nullptr == root) {
            return false;
        }
        if (nullptr == root->left && nullptr == root->right) {
            return sum == root->val;
        }
        return hasPathSum(root->left, sum - root->val) ||
               hasPathSum(root->right, sum - root->val);
    }
};
```

---

### 题目113:[路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

---

描述：
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

[思路](https://leetcode-cn.com/problems/path-sum-ii/solution/di-gui-ji-suan-lu-jing-zong-he-by-jarvis1890/)：

突破点：`DFS。`

步骤：

1. 递归记录当前路径上所有节点的值；
2. 当递归至叶子节点，计算路径总和并比较。

代码：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int> > ans;

    void dfs(TreeNode* root, int sum, vector<int> valVec){
        valVec.push_back(root->val);
        if(nullptr == root->left && nullptr == root->right){
            int s = 0;
            for(auto n: valVec) s += n;
            if(s == sum) ans.push_back(valVec);
        }
        if(root->left) dfs(root->left, sum, valVec);
        if(root->right) dfs(root->right, sum, valVec);
    }

    vector<vector<int> > pathSum(TreeNode* root, int sum) {
        if(root == NULL) return ans;
        dfs(root, sum, {});
        return ans; 
    }
};
```

---

### 题目235:[二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

---

描述：

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

示例 1:

输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
示例 2:

输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。


说明:

所有节点的值都是唯一的。
p、q 为不同节点且均存在于给定的二叉搜索树中。

[思路](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/solution/lca-by-ai-mao-de-xiao-gen-ban/)：

突破点：`递归。`

步骤：

1. 分左右两边进行递归；
2. 如果左边没有找到，说明公共祖先在右边；
3. 如果右边没有找到，说明公共祖先在左边；
4. 如果左右均不为空，则说明找到了。

代码：

```c++
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
				//递归边界返回空或者返回存在的那个结点
        if(nullptr == root || root == p || root == q) return root;
				//左边找一找
        TreeNode* leftNode = lowestCommonAncestor(root->left,p,q);
				//右边找一找
        TreeNode* rightNode = lowestCommonAncestor(root->right,p,q);
				//返回NULL或者有的那一侧
        if(nullptr == leftNode)return rightNode;
        if(nullptr == rightNode)return leftNode;
				//当前祖先左边有p，右边有q
        return root;  
}
```

---

### 题目1382:[将二叉搜索树变平衡](https://leetcode-cn.com/problems/balance-a-binary-search-tree/)

---

描述：

给你一棵二叉搜索树，请你返回一棵 平衡后 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。

如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 1 ，我们就称这棵二叉搜索树是 平衡的 。

如果有多种构造方法，请你返回任意一种。

示例：

输入：root = [1,null,2,null,3,null,4,null,null]
输出：[2,1,3,null,null,null,4]
解释：这不是唯一的正确答案，[3,1,4,null,2,null,null] 也是一个可行的构造方案。


提示：

树节点的数目在 1 到 10^4 之间。
树节点的值互不相同，且在 1 到 10^5 之间。

[思路](https://leetcode-cn.com/problems/balance-a-binary-search-tree/solution/di-gui-on-jie-fa-c-you-xian-dui-lie-by-time-limit/)：

突破点：`DFS。`

步骤：

1. 使用升序数组构造平衡二叉搜索树；
2. 设长度为n，则n/2处元素为根节点；
3. 递归进行构造。

代码：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
    void dfs(TreeNode *root, vector<int> &vec) {
        if(nullptr == root) { 
          return; 
        }
        dfs(root->left, vec);
        vec.push_back(root->val);
        dfs(root->right, vec);
    }
  
    TreeNode* construct(const vector<int> &vec, int leftVal, int rightVal) {
        if(leftVal > rightVal) {
            return nullptr;
        }
        int mid = (leftVal+rightVal)>>1;
        auto ptr = new TreeNode(vec[mid]);
        ptr->right = construct(vec, mid+1, rightVal);
        ptr->left = construct(vec, leftVal, mid-1);
        return ptr;
    }
  
public:
    TreeNode* balanceBST(TreeNode* root) {
        if(nullptr == root) {
            return nullptr;
        }
        vector<int> data;
        dfs(root, data);
        return construct(data, 0, data.size()-1);
    }
};
```

