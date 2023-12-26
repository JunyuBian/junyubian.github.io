---
title: LeetCode题目总结-Graph
date: 2020-09-12 21:32:19
categories: 
- LeetCode
tags:
- C++
- 算法
- ch
---

### 题目133:[克隆图](https://leetcode-cn.com/problems/clone-graph/)

---

描述：

给你无向连通图中一个节点的引用，请你返回该图的 深拷贝（克隆）。

图中的每个节点都包含它的值 val（int） 和其邻居的列表（list[Node]）。

class Node {
    public int val;
    public List<Node> neighbors;
}

测试用例格式：

简单起见，每个节点的值都和它的索引相同。例如，第一个节点值为 1（val = 1），第二个节点值为 2（val = 2），以此类推。该图在测试用例中使用邻接列表表示。

邻接列表 是用于表示有限图的无序列表的集合。每个列表都描述了图中节点的邻居集。

给定节点将始终是图中的第一个节点（值为 1）。你必须将给定节点的拷贝作为对克隆图的引用返回。

示例 1：

输入：adjList = [[2,4],[1,3],[2,4],[1,3]]
输出：[[2,4],[1,3],[2,4],[1,3]]
解释：
图中有 4 个节点。
节点 1 的值是 1，它有两个邻居：节点 2 和 4 。
节点 2 的值是 2，它有两个邻居：节点 1 和 3 。
节点 3 的值是 3，它有两个邻居：节点 2 和 4 。
节点 4 的值是 4，它有两个邻居：节点 1 和 3 。
示例 2：

输入：adjList = [[]]
输出：[[]]
解释：输入包含一个空列表。该图仅仅只有一个值为 1 的节点，它没有任何邻居。
示例 3：

输入：adjList = []
输出：[]
解释：这个图是空的，它不含任何节点。
示例 4：

输入：adjList = [[2],[1]]
输出：[[2],[1]]


提示：

节点数不超过 100 。
每个节点值 Node.val 都是唯一的，1 <= Node.val <= 100。
无向图是一个简单图，这意味着图中没有重复的边，也没有自环。
由于图是无向的，如果节点 p 是节点 q 的邻居，那么节点 q 也必须是节点 p 的邻居。
图是连通图，你可以从给定节点访问到所有节点。

[思路一](https://leetcode-cn.com/problems/clone-graph/solution/ke-long-tu-by-leetcode-solution/)：

突破点：`深度优先遍历。`

步骤：

1. 使用一个哈希表存储所有已被访问和克隆的节点，key对应原始节点，value对应克隆图中的节点；
2. 从给定节点开始遍历图，如果某个节点已经被访问过，则返回其克隆图中对应节点；
3. 如果当前访问的节点不在哈希表中，则创建它的克隆节点并保存在哈希表中；
4. 递归调用每个节点的邻接点。

代码：

```c++
class Solution {
public:
    unordered_map<Node*, Node*> visited;
    Node* cloneGraph(Node* node) {
        if (node == nullptr) {
            return node;
        }

        // 如果该节点已经被访问过了，则直接从哈希表中取出对应的克隆节点返回
        if (visited.find(node) != visited.end()) {
            return visited[node];
        }

        // 克隆节点，注意到为了深拷贝我们不会克隆它的邻居的列表
        Node* cloneNode = new Node(node->val);
        // 哈希表存储
        visited[node] = cloneNode;

        // 遍历该节点的邻居并更新克隆节点的邻居列表
        for (auto& neighbor: node->neighbors) {
            cloneNode->neighbors.emplace_back(cloneGraph(neighbor));
        }
        return cloneNode;
    }
};
```

[思路二](https://leetcode-cn.com/problems/clone-graph/solution/ke-long-tu-by-leetcode-solution/)：

突破点：`广度优先遍历。`

步骤：

1. 使用一个哈希表存储所有已被访问和克隆的节点，key对应原始节点，value对应克隆图中的节点；
2. 将题目给定节点添加到队列，克隆该节点并存储到哈希表中；
3. 每次从队首取一个节点，遍历其所有邻接点；
4. 如果某个邻接点已被访问，则从visited中取出；
5. 否则创建新的节点进行存储；
6. 重复操作直到队列为空。

代码：

```c++
class Solution {
public:
    Node* cloneGraph(Node* node) {
        if (node == nullptr) {
            return node;
        }

        unordered_map<Node*, Node*> visited;

        // 将题目给定的节点添加到队列
        queue<Node*> Q;
        Q.push(node);
        // 克隆第一个节点并存储到哈希表中
        visited[node] = new Node(node->val);

        // 广度优先搜索
        while (!Q.empty()) {
            // 取出队列的头节点
            auto n = Q.front();
            Q.pop();
            // 遍历该节点的邻居
            for (auto& neighbor: n->neighbors) {
                if (visited.find(neighbor) == visited.end()) {
                    // 如果没有被访问过，就克隆并存储在哈希表中
                    visited[neighbor] = new Node(neighbor->val);
                    // 将邻居节点加入队列中
                    Q.push(neighbor);
                }
                // 更新当前节点的邻居列表
                visited[n]->neighbors.emplace_back(visited[neighbor]);
            }
        }

        return visited[node];
    }
};
```

---

### 题目310:[最小高度树](https://leetcode-cn.com/problems/minimum-height-trees/)

---

描述：

对于一个具有树特征的无向图，我们可选择任何一个节点作为根。图因此可以成为树，在所有可能的树中，具有最小高度的树被称为最小高度树。给出这样的一个图，写出一个函数找到所有的最小高度树并返回他们的根节点。

格式

该图包含 n 个节点，标记为 0 到 n - 1。给定数字 n 和一个无向边 edges 列表（每一个边都是一对标签）。

你可以假设没有重复的边会出现在 edges 中。由于所有的边都是无向边， [0, 1]和 [1, 0] 是相同的，因此不会同时出现在 edges 里。

示例 1:

输入: n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3 

输出: [1]
示例 2:

输入: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5 

输出: [3, 4]
说明:

根据树的定义，树是一个无向图，其中任何两个顶点只通过一条路径连接。 换句话说，一个任何没有简单环路的连通图都是一棵树。
树的高度是指根节点和叶子节点之间最长向下路径上边的数量。

[思路](https://leetcode-cn.com/problems/minimum-height-trees/solution/c-9623-jian-ji-yi-dong-tuo-bu-pai-xu-bian-shi-by-t/)：

突破点：`拓扑排序。`

步骤：

1. 使用拓扑排序，不断缩小图，至只剩下1或2个点；
2. 在一个循环中，删除无向图中入度为1的点。

代码：

```c++
class Solution {
public:
vector<int> findMinHeightTrees(int n, vector<vector<int> >& edges) {
	if (n == 1)
		return { 0 };
	else if (n == 2)
		return{ 0,1 };
  
	//入度数组，并初始化
	vector<int> indegree(n,0);
	vector<int> v;
  //图形表示，并初始化
	vector<vector<int> > graph(n,v);
  //构造图与入度数组：无向图，两个点都要处理
	for (int i = 0; i < edges.size(); i++) {
		graph[edges[i][0]].push_back(edges[i][1]);
		graph[edges[i][1]].push_back(edges[i][0]);
		indegree[edges[i][0]]++;
		indegree[edges[i][1]]++;
	}
  //装载入度为1的queue
	queue<int> myqueue;
	for (int i = 0; i < n; i++) {
		if (indegree[i] == 1)
			myqueue.push(i);
	}
  //！！令cnt等于myqueue.size()，一次性将入度为1的点全部删去。
	int cnt = myqueue.size();
	while (n>2) {
    //一次性将入度为一的点全部删去！！不能一个一个删！
		n -= cnt;
		while (cnt--) {
			int temp = myqueue.front();
			myqueue.pop();
			indegree[temp] = 0;
			//更新temp的邻接点：若temp临接点的入度为1，则将其放入queue中。
			for (int i = 0; i < graph[temp].size(); i++) {
				if (indegree[graph[temp][i]] != 0) {
					indegree[graph[temp][i]]--;
					if (indegree[graph[temp][i]] == 1)//放在这里做！只判断邻接点。
						myqueue.push(graph[temp][i]);
				}
				
			}
		}
		cnt = myqueue.size();
	}
	vector<int> result;
	while (!myqueue.empty()){
		result.push_back(myqueue.front());
		myqueue.pop();
	}
	return result;
}
};
```

---

### 题目332:[重新安排行程](https://leetcode-cn.com/problems/reconstruct-itinerary/)

---

描述：

给定一个机票的字符串二维数组 [from, to]，子数组中的两个成员分别表示飞机出发和降落的机场地点，对该行程进行重新规划排序。所有这些机票都属于一个从 JFK（肯尼迪国际机场）出发的先生，所以该行程必须从 JFK 开始。

提示：

如果存在多种有效的行程，请你按字符自然排序返回最小的行程组合。例如，行程 ["JFK", "LGA"] 与 ["JFK", "LGB"] 相比就更小，排序更靠前
所有的机场都用三个大写字母表示（机场代码）。
假定所有机票至少存在一种合理的行程。
所有的机票必须都用一次 且 只能用一次。


示例 1：

输入：[["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
输出：["JFK", "MUC", "LHR", "SFO", "SJC"]
示例 2：

输入：[["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
输出：["JFK","ATL","JFK","SFO","ATL","SFO"]
解释：另一种有效的行程是 ["JFK","SFO","ATL","JFK","ATL","SFO"]。但是它自然排序更大更靠后。

[思路一](https://leetcode-cn.com/problems/reconstruct-itinerary/solution/zhong-xin-an-pai-xing-cheng-by-leetcode-solution/)：

突破点：`Hierholzer 算法（寻找欧拉路径）。`

步骤：

1. 从起点出发，进行深度优先搜索；
2. 每次沿着某条边从某个顶点移动到另外一个顶点时，删除这条边；
3. 如果没有可移动的路径，则将所在节点加入栈并返回；
4. 对于出入度差为1的节点，可能产生死胡同，最后入栈。 

代码：

```c++
class Solution {
public:
    unordered_map<string, priority_queue<string, vector<string>, std::greater<string> > > vec;

    vector<string> stk;

    void dfs(const string& curr) {
        while (vec.count(curr) && vec[curr].size() > 0) {
            string tmp = vec[curr].top();
            vec[curr].pop();
            dfs(move(tmp));
        }
        stk.emplace_back(curr);
    }

    vector<string> findItinerary(vector<vector<string> >& tickets) {
        for (auto& it : tickets) {
            vec[it[0]].emplace(it[1]);
        }
        dfs("JFK");

        reverse(stk.begin(), stk.end());
        return stk;
    }
};
```

[思路二](https://leetcode-cn.com/problems/reconstruct-itinerary/solution/332-zhong-xin-an-pai-xing-cheng-hui-su-fa-shen-sou/)：

突破点：`回溯。`

步骤：

1. 使用unordered_map记录城市间的映射；
2. 回溯遍历时，遇到的机场个数达到航班数量+1，则终止回溯。

代码：

```c++
class Solution {
private:
// unordered_map<出发城市, map<到达城市, 航班次数>> targets
unordered_map<string, map<string, int> > targets;
bool backtracking(int ticketNum, vector<string>& result) {
    if (result.size() == ticketNum + 1) {
        return true;
    }
    for (pair<const string, int>& target : targets[result[result.size() - 1]]) {
        if (target.second > 0 ) { // 使用int字段来记录到达城市是否使用过了
            result.push_back(target.first);
            target.second--;
            if (backtracking(ticketNum, result)) return true;
            result.pop_back();
            target.second++;
        }
    }
    return false;
}
public:
    vector<string> findItinerary(vector<vector<string>>& tickets) {
        vector<string> result;
        for (const vector<string>& vec : tickets) {
            targets[vec[0]][vec[1]]++; // 记录映射关系
        }
        result.push_back("JFK");
        backtracking(tickets.size(), result);
        return result;
    }
};
```

---

### 题目684:[冗余连接](https://leetcode-cn.com/problems/redundant-connection/)

---

描述：

在本问题中, 树指的是一个连通且无环的无向图。

输入一个图，该图由一个有着N个节点 (节点值不重复1, 2, ..., N) 的树及一条附加的边构成。附加的边的两个顶点包含在1到N中间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组。每一个边的元素是一对[u, v] ，满足 u < v，表示连接顶点u 和v的无向图的边。

返回一条可以删去的边，使得结果图是一个有着N个节点的树。如果有多个答案，则返回二维数组中最后出现的边。答案边 [u, v] 应满足相同的格式 u < v。

示例 1：

输入: [[1,2], [1,3], [2,3]]
输出: [2,3]
解释: 给定的无向图为:
  1
 / \
2 - 3
示例 2：

输入: [[1,2], [2,3], [3,4], [1,4], [1,5]]
输出: [1,4]
解释: 给定的无向图为:
5 - 1 - 2
    |   |
    4 - 3
注意:

输入的二维数组大小在 3 到 1000。
二维数组中的整数在1到N之间，其中N是输入数组的大小。

[思路](https://leetcode-cn.com/problems/redundant-connection/solution/684-rong-yu-lian-jie-bing-cha-ji-shi-xian-by-xiao-/)：

突破点：`并查集。`

步骤：

1. 遍历所有边，将连通的节点放入同一个集合，形成连通分量；
2. 遍历过程中，如果某一边的两个节点已经属于同一连通分量，则为冗余边。

代码：

```c++
class Solution {
private:
    int parent[1001];
    int find_root(int x) {
        while (parent[x] != x) {
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }
    bool union_root(int x, int y) {
        int root_x = find_root(x);
        int root_y = find_root(y);
        if (root_x == root_y) {
            return false;
        }
        parent[root_x] = root_y;
        return true;
    }    
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        for (int i = 1; i <= 1000; i++) {
            parent[i] = i;
        }        
        for (auto edge : edges) {
            if (!union_root(edge[0], edge[1])) {
                return edge;
            }
        }
        return {};
    }
};
```

---

### 题目685:[冗余连接 II](https://leetcode-cn.com/problems/redundant-connection-ii/)

---

描述：

在本问题中，有根树指满足以下条件的有向图。该树只有一个根节点，所有其他节点都是该根节点的后继。每一个节点只有一个父节点，除了根节点没有父节点。

输入一个有向图，该图由一个有着N个节点 (节点值不重复1, 2, ..., N) 的树及一条附加的边构成。附加的边的两个顶点包含在1到N中间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组。 每一个边 的元素是一对 [u, v]，用以表示有向图中连接顶点 u 和顶点 v 的边，其中 u 是 v 的一个父节点。

返回一条能删除的边，使得剩下的图是有N个节点的有根树。若有多个答案，返回最后出现在给定二维数组的答案。

示例 1:

输入: [[1,2], [1,3], [2,3]]
输出: [2,3]
解释: 给定的有向图如下:
  1
 / \
v   v
2-->3
示例 2:

输入: [[1,2], [2,3], [3,4], [4,1], [1,5]]
输出: [4,1]
解释: 给定的有向图如下:
5 <- 1 -> 2
     ^    |
     |    v
     4 <- 3
注意:

二维数组大小的在3到1000范围内。
二维数组中的每个整数在1到N之间，其中 N 是二维数组的大小。

[思路](https://leetcode-cn.com/problems/redundant-connection-ii/solution/zui-jian-dan-fang-fa-bu-yong-fen-lei-yi-kan-jiu-do/)：

突破点：`并查集。`

步骤：

1. 遍历一遍寻找入读为2的点，记录为root；
2. 遍历第二遍，将非指向root的边用并查集合并，指向root的边用数组记录；
3. 遍历数组记录的点，判断该点是否与root指向同一点；
4. 若不是，说明没有联通，进行合并；
5. 若指向同一点，说明\[该点, root]的边冗余，可以删去；
6. 当入度全为1， 返回环中最后出现的边即可。

代码：

```c++
class Solution {
public:
    int pre[1005],ind[1005];
    int find(int x){
        return pre[x]==x?x:pre[x]=find(pre[x]);
    }
    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int n=edges.size(),root=-1;
        vector<int> v;
        for(int i=1;i<=n;++i) pre[i]=i;
        for(auto i:edges){
            ind[i[1]]++;
            if(ind[i[1]]==2)
                root=i[1];
        }
        if(root == -1) {
            for(auto i : edges) {
                int a = find(i[0]), b = find(i[1]);
                if(a != b) pre[b] = a;
                else return i;
            }
        }
        for(auto i:edges){
            if(i[1]!=root){
                pre[find(i[1])]=find(i[0]);
            }
            else
                v.emplace_back(i[0]);
        }
        if(find(root)!=find(v[0]))
            return {v[1],root};
        else
            return {v[0],root};
    }
};
```

