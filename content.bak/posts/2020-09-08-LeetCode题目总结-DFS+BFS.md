---
title: LeetCode题目总结-DFS+BFS
date: 2020-09-08 14:03:19
categories:
- LeetCode
- Ch
tags:
- C++
- 算法
---

### 题目116:[填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

描述：

给定一个完美二叉树，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

<!--more-->

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

示例：

输入：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":null,"right":null,"val":4},"next":null,"right":{"$id":"4","left":null,"next":null,"right":null,"val":5},"val":2},"next":null,"right":{"$id":"5","left":{"$id":"6","left":null,"next":null,"right":null,"val":6},"next":null,"right":{"$id":"7","left":null,"next":null,"right":null,"val":7},"val":3},"val":1}

输出：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":{"$id":"4","left":null,"next":{"$id":"5","left":null,"next":{"$id":"6","left":null,"next":null,"right":null,"val":7},"right":null,"val":6},"right":null,"val":5},"right":null,"val":4},"next":{"$id":"7","left":{"$ref":"5"},"next":null,"right":{"$ref":"6"},"val":3},"right":{"$ref":"4"},"val":2},"next":null,"right":{"$ref":"7"},"val":1}

提示：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

[思路](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/solution/dui-lie-mo-ni-yan-du-bian-li-shi-jian-97kong-jian-/)：

突破点：`广度优先搜索。`

步骤：

1. 使用队列进行广度优先遍历；
2. 在接点出队列后，next指向队列首个元素，广度遍历完直接return。

代码：

```c++
class Solution {
public:
    Node* connect(Node* root) {
    	if(!root) return root;
    	queue<Node*> work;
      work.push(root);
    	work.push(nullptr);
    	Node* cur = nullptr;
    	while(1) {
        // 如果队列首部是结点
        if(work.front()) {
        	cur = work.front();
    			work.pop();
          // 如果是非叶子结点
          if(cur->left) {
          	work.push(cur->left);
    				work.push(cur->right);
          }
    			cur->next = work.front();
        }
        // 如果只剩下一个nullptr结点
    		else if (1 == work.size()) {
          return root;
        }
        // 如果遇到nullptr结点，这是一层的分割点
    		else {
    			work.pop();
    			work.push(nullptr);
    		}
    	}
      return root;
    }
};
```

---

### 题目117:[填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

描述：

给定一个二叉树

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

进阶：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。


示例：

输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]


提示：

树中的节点数小于 6000
-100 <= node.val <= 100

[思路](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/solution/cceng-ci-bian-li-by-mrnice/)：

突破点：`层次遍历。`

步骤：

1. 使用队列层次遍历；
2. 每循环一层将这一层清空，录入孩子节点。

代码：

```c++
class Solution {
public:
    Node* connect(Node* root) {
        if(!root) {
          return root;
        }
        queue<Node*> q{{root}};
        while(!q.empty()) {
            int n = q.size();
            for(int i = 0; i < n; i++){
                Node* t = q.front();
                q.pop();
                if(n-1 != i){
                    Node* tNext = q.front();
                    t->next = tNext;
                }
                if(t->left) {
                  q.push(t->left);
                }
                if(t->right) {
                  q.push(t->right);
                }
            }
        }
        return root;
    }
};
```

---

### 题目200:[岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

描述：

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

示例 1:

输入:
[
['1','1','1','1','0'],
['1','1','0','1','0'],
['1','1','0','0','0'],
['0','0','0','0','0']
]
输出: 1
示例 2:

输入:
[
['1','1','0','0','0'],
['1','1','0','0','0'],
['0','0','1','0','0'],
['0','0','0','1','1']
]
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。

[思路一](https://leetcode-cn.com/problems/number-of-islands/solution/dao-yu-shu-liang-by-leetcode/)：

突破点：`深度优先搜索。`

步骤：

1. 将二维网格视为无向图，相邻1之间有边相连；
2. 搜索到1，则标记为0；
3. 最终深度优先搜索次数即为岛屿数量。

代码：

```c++
class Solution {
private:
    void dfs(vector<vector<char> >& grid, int r, int c) {
        int nr = grid.size();
        int nc = grid[0].size();

        grid[r][c] = '0';
        if ('1' == r - 1 >= 0 && grid[r-1][c]) dfs(grid, r - 1, c);
        if ('1' == r + 1 < nr && grid[r+1][c]) dfs(grid, r + 1, c);
        if ('1' == c - 1 >= 0 && grid[r][c-1]) dfs(grid, r, c - 1);
        if ('1' == c + 1 < nc && grid[r][c+1]) dfs(grid, r, c + 1);
    }

public:
    int numIslands(vector<vector<char> >& grid) {
        int nr = grid.size();
        if (!nr) return 0;
        int nc = grid[0].size();

        int num_islands = 0;
        for (int r = 0; r < nr; ++r) {
            for (int c = 0; c < nc; ++c) {
                if ('1' == grid[r][c]) {
                    ++num_islands;
                    dfs(grid, r, c);
                }
            }
        }
        return num_islands;
    }
};
```

[思路二](https://leetcode-cn.com/problems/number-of-islands/solution/dao-yu-shu-liang-by-leetcode/)：

突破点：`广度优先搜索。`

步骤：

1. 将二维网格视为无向图，相邻1之间有边相连；
2. 搜索到1，则加入队列，并修改标记为0；
3. 最终广度优先搜索次数即为岛屿数量。

代码：

```c++
class Solution {
public:
    int numIslands(vector<vector<char> >& grid) {
        int nr = grid.size();
        if (!nr) return 0;
        int nc = grid[0].size();

        int num_islands = 0;
        for (int r = 0; r < nr; ++r) {
            for (int c = 0; c < nc; ++c) {
                if (grid[r][c] == '1') {
                  ++num_islands;
                  grid[r][c] = '0';
                  queue<pair<int, int> > neighbors;
                  neighbors.push({r, c});
                  while (!neighbors.front()) {
                    auto rc = neighbors.front();
                    neighbors.pop();
                    int row = rc.first, col = rc.second;
                    if (0 <= row - 1 && '1' == grid[row-1][col]) {
                      neighbors.push({row-1, col});
                      grid[row-1][col] = '0';
                    }
                    if (row + 1 < nr && grid[row+1][col] == '1') {
                      neighbors.push({row+1, col});
                      grid[row+1][col] = '0';
                    }
                    if (col - 1 >= 0 && grid[row][col-1] == '1') {
                      neighbors.push({row, col-1});
                      grid[row][col-1] = '0';
                    }
                    if (col + 1 < nc && grid[row][col+1] == '1') {
                      neighbors.push({row, col+1});
                      grid[row][col+1] = '0';
                    }
                  }
                }
            }
        }
        return num_islands;
    }
};
```

---

### 题目207:[课程表](https://leetcode-cn.com/problems/course-schedule/)

描述：

你这个学期必须选修 numCourse 门课程，记为 0 到 numCourse-1 。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们：[0,1]

给定课程总量以及它们的先决条件，请你判断是否可能完成所有课程的学习？

示例 1:

输入: 2, [[1,0]]
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
示例 2:

输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。


提示：

输入的先决条件是由 边缘列表 表示的图形，而不是 邻接矩阵 。详情请参见图的表示法。
你可以假定输入的先决条件中没有重复的边。
1 <= numCourses <= 10^5

[思路一](https://leetcode-cn.com/problems/course-schedule/solution/ke-cheng-biao-by-leetcode-solution/)：

突破点：`深度优先搜索。`

步骤：

1. 题目即寻找有向图中是否成环；
2. 通过深度优先搜索，寻找拓扑排序；
3. 如果存在，说明无环，如果不存在，说明有环。

代码：

```c++
class Solution {
private:
    vector<vector<int> > edges;
    vector<int> visited;
    bool valid = true;

public:
    void dfs(int u) {
        visited[u] = 1;
        for (int v: edges[u]) {
            if (0 == visited[v]) {
                dfs(v);
                if (!valid) {
                    return;
                }
            } else if (1 == visited[v]) {
                valid = false;
                return;
            }
        }
        visited[u] = 2;
    }

    bool canFinish(int numCourses, vector<vector<int> >& prerequisites) {
        edges.resize(numCourses);
        visited.resize(numCourses);
        for (const auto& info: prerequisites) {
            edges[info[1]].push_back(info[0]);
        }
        for (int i = 0; i < numCourses && valid; ++i) {
            if (!visited[i]) {
                dfs(i);
            }
        }
        return valid;
    }
};
```

[思路二](https://leetcode-cn.com/problems/course-schedule/solution/ke-cheng-biao-by-leetcode-solution/)：

突破点：`广度优先搜索。`

步骤：

1. 题目即寻找有向图中是否成环；
2. 通过广度优先搜索，寻找拓扑排序；
3. 寻找所有入度为0的点放入队列；
4. 每一步广度优先搜索时，取出队首节点，加入答案中；
5. 移除该点的所有出边；
6. 如果有某个相邻节点入度变为0，则将该节点加入答案；
7. 结束后，如果答案包含n各节点，则找到一种拓扑排序；
8. 否则，说明存在环。

代码：

```c++
class Solution {
private:
    vector<vector<int> > edges;
    vector<int> indeg;

public:
    bool canFinish(int numCourses, vector<vector<int> >& prerequisites) {
        edges.resize(numCourses);
        indeg.resize(numCourses);
        for (const auto& info: prerequisites) {
            edges[info[1]].push_back(info[0]);
            ++indeg[info[0]];
        }

        queue<int> q;
        for (int i = 0; i < numCourses; ++i) {
            if (0 == indeg[i]) {
                q.push(i);
            }
        }

        int visited = 0;
        while (!q.empty()) {
            ++visited;
            int u = q.front();
            q.pop();
            for (int v: edges[u]) {
                --indeg[v];
                if (0 == indeg[v]) {
                    q.push(v);
                }
            }
        }
        return visited == numCourses;
    }
};
```

---

### 题目210:[课程表 II](https://leetcode-cn.com/problems/course-schedule-ii/)

描述：

现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: [0,1]

给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。

示例 1:

输入: 2, [[1,0]]
输出: [0,1]
解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。
示例 2:

输入: 4, [[1,0],[2,0],[3,1],[3,2]]
输出: [0,1,2,3] or [0,2,1,3]
解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。
说明:

输入的先决条件是由边缘列表表示的图形，而不是邻接矩阵。详情请参见图的表示法。
你可以假定输入的先决条件中没有重复的边。
提示:

这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
通过 DFS 进行拓扑排序 - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
拓扑排序也可以通过 BFS 完成。

[思路](https://leetcode-cn.com/problems/course-schedule-ii/solution/ke-cheng-biao-ii-by-leetcode-solution/)：

突破点：`深度优先搜索。`

步骤：

1. 思考过程与题目207类似；
2. 当我们标记当前节点u为”搜索中“后，遍历每个相邻节点v；
3. 如果为未搜索，则开始搜索v，搜索完成后回溯到u；
4. 如果为搜索中，则找到一个环，返回false；
5. 如果为已完成，说明v已经在栈中，不进行操作；
6. u所有相邻节点都为”已完成“后，将u入栈，并标记为已完成。

代码：

```c++
class Solution {
private:
    // 存储有向图
    vector<vector<int> > edges;
    // 标记每个节点的状态：0=未搜索，1=搜索中，2=已完成
    vector<int> visited;
    // 用数组来模拟栈，下标 0 为栈底，n-1 为栈顶
    vector<int> result;
    // 判断有向图中是否有环
    bool valid = true;

public:
    void dfs(int u) {
        // 将节点标记为「搜索中」
        visited[u] = 1;
        // 搜索其相邻节点
        // 只要发现有环，立刻停止搜索
        for (int v: edges[u]) {
            // 如果「未搜索」那么搜索相邻节点
            if (visited[v] == 0) {
                dfs(v);
                if (!valid) {
                    return;
                }
            }
            // 如果「搜索中」说明找到了环
            else if (visited[v] == 1) {
                valid = false;
                return;
            }
        }
        // 将节点标记为「已完成」
        visited[u] = 2;
        // 将节点入栈
        result.push_back(u);
    }

    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        edges.resize(numCourses);
        visited.resize(numCourses);
        for (const auto& info: prerequisites) {
            edges[info[1]].push_back(info[0]);
        }
        // 每次挑选一个「未搜索」的节点，开始进行深度优先搜索
        for (int i = 0; i < numCourses && valid; ++i) {
            if (!visited[i]) {
                dfs(i);
            }
        }
        if (!valid) {
            return {};
        }
        // 如果没有环，那么就有拓扑排序
        // 注意下标 0 为栈底，因此需要将数组反序输出
        reverse(result.begin(), result.end());
        return result;
    }
};
```

---

### 题目279:[完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

描述：

给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

示例 1:

输入: n = 12
输出: 3
解释: 12 = 4 + 4 + 4.
示例 2:

输入: n = 13
输出: 2
解释: 13 = 4 + 9.

[思路一](https://leetcode-cn.com/problems/perfect-squares/solution/dong-tai-gui-hua-bfsliang-chong-fang-fa-by-yu-mu-2/)：

突破点：`广度优先搜索。`

步骤：

1. 将题目抽象为从n走到0，每次跨越平方距离，求最少跨越次数；
2. 使用BFS解决。

代码：

```c++
class Solution {
public:
    /*返回小于n的平方序列: 1, 4, 9...*/
    vector<int> getSquares(int n) {
        vector<int> res;
        for(int i = 1; i*i <= n; ++i) {
            res.push_back(i*i);
        }
        return res;
    }

    int numSquares(int n) {
        vector<int> squares = getSquares(n);
        vector<bool> visited(n+1);    //记录已访问过的节点
        queue<int> q;

        q.push(n);
        int res = 0;
        visited[n] = true;
        while(!q.empty()) {
            int size = q.size();
            res++;

            while(size--) {
                int curr = q.front();
                q.pop();
                /*每次跨越的间隔为平方数*/
                for(int num: squares) {
                    int next = curr - num;
                    if(0 > next) {
                        break;
                    }
                    if(0 == next) {
                        return res;
                    }
                    visited[next] = true;
                    q.push(next);
                }
            }
        }
        return n;
    }
};
```

[思路二](https://leetcode-cn.com/problems/perfect-squares/solution/yi-ge-wan-quan-bei-bao-wen-ti-by-wtffqbpl/)：

突破点：`动态规划。`

步骤：

1. 将题目理解为背包问题；
2. 背包容量v[i]表示每个完全平方数字的大小；
3. 背包价值w[i]为1；
4. 求解组成数组所需要的完全平方数数量最少即为背包的价值最低。

代码：

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> choices;
        int res = 1;

        // 构造物品，即所有小于给定数字的完全平方数
        while (n / res >= res) {
            choices.push_back(res * res);
            res++;
        }

        const int size = choices.size();
        vector<int> dp(n + 1, 0);

        // init
        for (int i = 0; i <= n; ++i) {
            dp[i] = i;
        }

        // 完全背包模板
        for (int i = 1; i < size; ++i) {
            for (int j = choices[i]; j <= n; ++j) {
                dp[j] = min(dp[j], dp[j - choices[i]] + 1);
            }
        }

        return dp[n];
    }
};
```

---

### 题目301:[删除无效的括号](https://leetcode-cn.com/problems/remove-invalid-parentheses/)

描述：

删除最小数量的无效括号，使得输入的字符串有效，返回所有可能的结果。

说明: 输入可能包含了除 ( 和 ) 以外的字符。

示例 1:

输入: "()())()"
输出: ["()()()", "(())()"]
示例 2:

输入: "(a)())()"
输出: ["(a)()()", "(a())()"]
示例 3:

输入: ")("
输出: [""]

[思路](https://leetcode-cn.com/problems/remove-invalid-parentheses/solution/dfsjie-ti-by-hw_wt/)：

突破点：`深度优先遍历。`

步骤：

1. 首先遍历输入字符串，获取需要删除的左右括号个数；
2. 递归循环进行左右删除；
3. 当1.中计数都为0时，检查输入字符串是否有效。

代码：

```c++
class Solution {
public:
    bool isvalid(string s) {
        int cnt = 0;
        for (auto c : s) {
            if (c == '(') {
                cnt++;
            } else if (c == ')') {
                cnt--;
                if (cnt < 0) return false;
            }
        }
        return cnt == 0;
    }

    void dfs(string s, int st, int l, int r, vector<string>& ans) {
        if (l == 0 && r == 0) {
            if (isvalid(s)) {
                ans.push_back(s);
            }
            return;
        }

        for (int i = st; i < s.size(); i++) {
            if (i != st && s[i] == s[i-1]) continue;
            if (s[i] == '(' && l > 0) {
              	// 删除操作，substr(a, b):从a开始个字符组成的字符串
                dfs(s.substr(0, i) + s.substr(i+1, s.size()-1-i), i, l - 1, r, ans);
            }
            if (s[i] == ')' && r > 0) {
              	// 删除操作，substr(a, b):从a开始个字符组成的字符串
                dfs(s.substr(0, i) + s.substr(i+1, s.size()-1-i), i, l, r - 1, ans);
            }
        }
    }

    vector<string> removeInvalidParentheses(string s) {
        int left = 0;
        int right = 0;
        vector<string> ans;

        for (auto c : s) {
            if (c == '(') {
                left++;
            } else if (c == ')') {
                if (left > 0) {
                    left--;
                } else {
                    right++;
                }
            }
        }
        // left和right表示左右括号要删除的个数
        dfs(s, 0, left, right, ans);
        return ans;
    }
};
```
