---
title: LeetCode题目总结-Queue+TopologicalSort
date: 2020-09-12 21:32:19
<<<<<<< HEAD
categories: 
- LeetCode
tags:
- C++
- 算法
- ch
=======
categories:
- LeetCode
- Ch
tags:
- C++
- 算法
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
---

### 题目621:[任务调度器](https://leetcode-cn.com/problems/task-scheduler/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个用字符数组表示的 CPU 需要执行的任务列表。其中包含使用大写的 A - Z 字母表示的26 种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。CPU 在任何一个单位时间内都可以执行一个任务，或者在待命状态。

然而，两个相同种类的任务之间必须有长度为 n 的冷却时间，因此至少有连续 n 个单位时间内 CPU 在执行不同的任务，或者在待命状态。

<!--more-->

你需要计算完成所有任务所需要的最短时间。

示例 ：

输入：tasks = ["A","A","A","B","B","B"], n = 2
输出：8
解释：A -> B -> (待命) -> A -> B -> (待命) -> A -> B.
<<<<<<< HEAD
在本示例中，两个相同类型任务之间必须间隔长度为 n = 2 的冷却时间，而执行一个任务只需要一个单位时间，所以中间出现了（待命）状态。 

=======
在本示例中，两个相同类型任务之间必须间隔长度为 n = 2 的冷却时间，而执行一个任务只需要一个单位时间，所以中间出现了（待命）状态。
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

提示：

任务的总个数为 [1, 10000]。
n 的取值范围为 [0, 100]。

[思路](https://leetcode-cn.com/problems/task-scheduler/solution/tong-zi-by-popopop/)：

突破点：`桶思想。`

步骤：

1. 建立大小为n+1的桶，个数为数量最多的任务；
2. 每个桶视为一轮任务；
3. 总排队时间=(桶个数-1)*(n+1)+最后一个桶的任务数；

代码：

```c++
int leastInterval(vector<char>& tasks, int n) {
        int len=tasks.size();
        vector<int> vec(26);
        for(char c:tasks) ++vec[c-'A'];
<<<<<<< HEAD
  
        sort(vec.begin(),vec.end(),[](int& x,int&y){return x>y;});
  
        int cnt=1;
  
=======

        sort(vec.begin(),vec.end(),[](int& x,int&y){return x>y;});

        int cnt=1;

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
        while(cnt<vec.size()&&vec[cnt]==vec[0]) cnt++;
        return max(len,cnt+(n+1)*(vec[0]-1) );
    }
```

---

### 题目641:[设计循环双端队列](https://leetcode-cn.com/problems/design-circular-deque/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

设计实现双端队列。
你的实现需要支持以下操作：

MyCircularDeque(k)：构造函数,双端队列的大小为k。
insertFront()：将一个元素添加到双端队列头部。 如果操作成功返回 true。
insertLast()：将一个元素添加到双端队列尾部。如果操作成功返回 true。
deleteFront()：从双端队列头部删除一个元素。 如果操作成功返回 true。
deleteLast()：从双端队列尾部删除一个元素。如果操作成功返回 true。
getFront()：从双端队列头部获得一个元素。如果双端队列为空，返回 -1。
getRear()：获得双端队列的最后一个元素。 如果双端队列为空，返回 -1。
isEmpty()：检查双端队列是否为空。
isFull()：检查双端队列是否满了。
示例：

MyCircularDeque circularDeque = new MycircularDeque(3); // 设置容量大小为3
circularDeque.insertLast(1);			        // 返回 true
circularDeque.insertLast(2);			        // 返回 true
circularDeque.insertFront(3);			        // 返回 true
circularDeque.insertFront(4);			        // 已经满了，返回 false
circularDeque.getRear();  				// 返回 2
circularDeque.isFull();				        // 返回 true
circularDeque.deleteLast();			        // 返回 true
circularDeque.insertFront(4);			        // 返回 true
circularDeque.getFront();				// 返回 4

提示：

所有值的范围为 [1, 1000]
操作次数的范围为 [1, 1000]
请不要使用内置的双端队列库。

[思路]()：

突破点：`双端链表。`

代码：

```c++
class MyCircularDeque {
public:
    struct DLNode {
        int val;
        DLNode* next;
        DLNode* prev;
        DLNode() : val(-1), next(NULL), prev(NULL) {}
        DLNode(int v) : val(v), next(NULL), prev(NULL) {}
    };
    int size;
    int capacity;
    DLNode* head;
    DLNode* tail;
    /** Initialize your data structure here. Set the size of the deque to be k. */
    MyCircularDeque(int k) {
        size = 0;
        capacity = k;
        head = new DLNode();
        tail = new DLNode();
        head->next = tail;
        tail->prev = head;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    bool insertFront(int value) {
        if (isFull()) return false;
        auto node = new DLNode(value);
        node->prev = head;
        node->next = head->next;
        node->next->prev = node;
        node->prev->next = node;
        ++size;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    bool insertLast(int value) {
        if (isFull()) return false;
        auto node = new DLNode(value);
        node->prev = tail->prev;
        node->next = tail;
        node->prev->next = node;
        node->next->prev = node;
        ++size;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    bool deleteFront() {
        if (isEmpty()) return false;
        auto node = head->next;
        node->next->prev = node->prev;
        node->prev->next = node->next;
        delete node;
        node = NULL;
        --size;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    bool deleteLast() {
        if (isEmpty()) return false;
        auto node = tail->prev;
        node->next->prev = node->prev;
        node->prev->next = node->next;
        delete node;
        node = NULL;
        --size;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Get the front item from the deque. */
    int getFront() {
        return head->next->val;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Get the last item from the deque. */
    int getRear() {
        return tail->prev->val;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Checks whether the circular deque is empty or not. */
    bool isEmpty() {
        return size == 0;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Checks whether the circular deque is full or not. */
    bool isFull() {
        return size == capacity;
    }
};
```

---

### 题目622:[设计循环队列](https://leetcode-cn.com/problems/design-circular-queue/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

设计你的循环队列实现。 循环队列是一种线性数据结构，其操作表现基于 FIFO（先进先出）原则并且队尾被连接在队首之后以形成一个循环。它也被称为“环形缓冲器”。

循环队列的一个好处是我们可以利用这个队列之前用过的空间。在一个普通队列里，一旦一个队列满了，我们就不能插入下一个元素，即使在队列前面仍有空间。但是使用循环队列，我们能使用这些空间去存储新的值。

你的实现应该支持如下操作：

MyCircularQueue(k): 构造器，设置队列长度为 k 。
Front: 从队首获取元素。如果队列为空，返回 -1 。
Rear: 获取队尾元素。如果队列为空，返回 -1 。
enQueue(value): 向循环队列插入一个元素。如果成功插入则返回真。
deQueue(): 从循环队列中删除一个元素。如果成功删除则返回真。
isEmpty(): 检查循环队列是否为空。
isFull(): 检查循环队列是否已满。


示例：

MyCircularQueue circularQueue = new MyCircularQueue(3); // 设置长度为 3
circularQueue.enQueue(1);  // 返回 true
circularQueue.enQueue(2);  // 返回 true
circularQueue.enQueue(3);  // 返回 true
circularQueue.enQueue(4);  // 返回 false，队列已满
circularQueue.Rear();  // 返回 3
circularQueue.isFull();  // 返回 true
circularQueue.deQueue();  // 返回 true
circularQueue.enQueue(4);  // 返回 true
circularQueue.Rear();  // 返回 4

<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
提示：

所有的值都在 0 至 1000 的范围内；
操作数将在 1 至 1000 的范围内；
请不要使用内置的队列库。

[思路](https://leetcode-cn.com/problems/design-circular-queue/solution/xun-huan-dui-lie-by-zheng-rui-jia/)：

突破点：`下标%数组大小。`

代码：

```c++
class MyCircularQueue {
private:
    int start;
    int end;
    int count;
    vector<int> nums;
<<<<<<< HEAD
  
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
public:
    /** Initialize your data structure here. Set the size of the queue to be k. */
    MyCircularQueue(int k):
        start(0),
        end(0),
        count(0)
    {
        nums.resize(k);
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Insert an element into the circular queue. Return true if the operation is successful. */
    bool enQueue(int value) {
        if (count == nums.size())
            return false;
        nums[start++] = value;
        start %= nums.size();
        ++count;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Delete an element from the circular queue. Return true if the operation is successful. */
    bool deQueue() {
        if (count == 0)
            return false;
        nums[end++] = 0;
        end %= nums.size();
        --count;
        return true;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Get the front item from the queue. */
    int Front() {
        if (count == 0)
            return -1;
        return nums[end];
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Get the last item from the queue. */
    int Rear() {
        if (count == 0)
            return -1;
        return nums[(start - 1 + nums.size()) % nums.size()];
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Checks whether the circular queue is empty or not. */
    bool isEmpty() {
        return count == 0;
    }
<<<<<<< HEAD
    
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
    /** Checks whether the circular queue is full or not. */
    bool isFull() {
        return nums.size() == count;
    }
};
```

---

### 题目329:[矩阵中的最长递增路径](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个整数矩阵，找出最长递增路径的长度。

对于每个单元格，你可以往上，下，左，右四个方向移动。 你不能在对角线方向上移动或移动到边界外（即不允许环绕）。

示例 1:

<<<<<<< HEAD
输入: nums = 
=======
输入: nums =
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
<<<<<<< HEAD
] 
输出: 4 
解释: 最长递增路径为 [1, 2, 6, 9]。
示例 2:

输入: nums = 
=======
]
输出: 4
解释: 最长递增路径为 [1, 2, 6, 9]。
示例 2:

输入: nums =
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
<<<<<<< HEAD
] 
输出: 4 
=======
]
输出: 4
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
解释: 最长递增路径是 [3, 4, 5, 6]。注意不允许在对角线方向上移动。

[思路一](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/solution/ju-zhen-zhong-de-zui-chang-di-zeng-lu-jing-by-le-2/)：

突破点：`优化的深度优先搜索。`

步骤：

1. 将矩阵视为有向图，若相邻两个单元格大小不等，则在两相邻单元格中存在一条小值指向大值的有向边；
2. 在有向图中，寻找最长路径；
3. 从一个单元格开始DFS，直到搜索结束；
4. 使用缓存矩阵优化，已经计算过的单元格进行保存。

代码：

```c++
class Solution {
public:
    static constexpr int dirs[4][2] = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    int rows, columns;

    int longestIncreasingPath(vector< vector<int> > &matrix) {
        if (matrix.size() == 0 || matrix[0].size() == 0) {
            return 0;
        }
        rows = matrix.size();
        columns = matrix[0].size();
        auto memo = vector< vector<int> > (rows, vector <int> (columns));
        int ans = 0;
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < columns; ++j) {
                ans = max(ans, dfs(matrix, i, j, memo));
            }
        }
        return ans;
    }

    int dfs(vector< vector<int> > &matrix, int row, int column, vector< vector<int> > &memo) {
        if (memo[row][column] != 0) {
            return memo[row][column];
        }
        ++memo[row][column];
        for (int i = 0; i < 4; ++i) {
            int newRow = row + dirs[i][0], newColumn = column + dirs[i][1];
            if (newRow >= 0 && newRow < rows && newColumn >= 0 && newColumn < columns && matrix[newRow][newColumn] > matrix[row][column]) {
                memo[row][column] = max(memo[row][column], dfs(matrix, newRow, newColumn, memo) + 1);
            }
        }
        return memo[row][column];
    }
};
```

[思路二](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/solution/ju-zhen-zhong-de-zui-chang-di-zeng-lu-jing-by-le-2/)：

突破点：`拓扑排序+动态规划。`

步骤：

1. 状态转移方程：memo\[i]\[j] = max\{memo\[x]\[y]} + 1，(x, y)与(i, j)相邻，且matrix\[x]\[y]>matrix\[i]\[j]；
2. 使用拓扑排序，从所有出度为0的单元格开始DFS；
3. 更新其余单元格出度，并将出度为0的加入下一层搜索；
4. 搜索结束后，总层数即为所求答案。

代码：

```c++
class Solution {
public:
    static constexpr int dirs[4][2] = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    int rows, columns;

    int longestIncreasingPath(vector< vector<int> > &matrix) {
        if (matrix.size() == 0 || matrix[0].size() == 0) {
            return 0;
        }
        rows = matrix.size();
        columns = matrix[0].size();
        auto outdegrees = vector< vector<int> > (rows, vector <int> (columns));
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < columns; ++j) {
                for (int k = 0; k < 4; ++k) {
                    int newRow = i + dirs[k][0], newColumn = j + dirs[k][1];
                    if (newRow >= 0 && newRow < rows && newColumn >= 0 && newColumn < columns && matrix[newRow][newColumn] > matrix[i][j]) {
                        ++outdegrees[i][j];
                    }
                }
            }
        }
        queue < pair<int, int> > q;
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < columns; ++j) {
                if (outdegrees[i][j] == 0) {
                    q.push({i, j});
                }
            }
        }
        int ans = 0;
        while (!q.empty()) {
            ++ans;
            int size = q.size();
            for (int i = 0; i < size; ++i) {
                auto cell = q.front(); q.pop();
                int row = cell.first, column = cell.second;
                for (int k = 0; k < 4; ++k) {
                    int newRow = row + dirs[k][0], newColumn = column + dirs[k][1];
                    if (newRow >= 0 && newRow < rows && newColumn >= 0 && newColumn < columns && matrix[newRow][newColumn] < matrix[row][column]) {
                        --outdegrees[newRow][newColumn];
                        if (outdegrees[newRow][newColumn] == 0) {
                            q.push({newRow, newColumn});
                        }
                    }
                }
            }
        }
        return ans;
    }
};
```

---

### 题目1203:[项目管理](https://leetcode-cn.com/problems/sort-items-by-groups-respecting-dependencies/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

公司共有 n 个项目和  m 个小组，每个项目要不没有归属，要不就由其中的一个小组负责。

我们用 group[i] 代表第 i 个项目所属的小组，如果这个项目目前无人接手，那么 group[i] 就等于 -1。（项目和小组都是从零开始编号的）

请你帮忙按要求安排这些项目的进度，并返回排序后的项目列表：

同一小组的项目，排序后在列表中彼此相邻。
项目之间存在一定的依赖关系，我们用一个列表 beforeItems 来表示，其中 beforeItems[i] 表示在进行第 i 个项目前（位于第 i 个项目左侧）应该完成的所有项目。
结果要求：

如果存在多个解决方案，只需要返回其中任意一个即可。

如果没有合适的解决方案，就请返回一个 空列表

示例 1：

输入：n = 8, m = 2, group = [-1,-1,1,0,0,1,0,-1], beforeItems = [[],[6],[5],[6],[3,6],[],[],[]]
输出：[6,3,4,1,5,2,0,7]
示例 2：

输入：n = 8, m = 2, group = [-1,-1,1,0,0,1,0,-1], beforeItems = [[],[6],[5],[6],[3],[],[4],[]]
输出：[]
解释：与示例 1 大致相同，但是在排序后的列表中，4 必须放在 6 的前面。


提示：

1 <= m <= n <= 3*10^4
group.length == beforeItems.length == n
-1 <= group[i] <= m-1
0 <= beforeItems[i].length <= n-1
0 <= beforeItems\[i]\[j] <= n-1
i != beforeItems\[i]\[j]

[思路](https://leetcode-cn.com/problems/sort-items-by-groups-respecting-dependencies/solution/chuang-jian-xin-zu-fen-qu-yu-jin-xing-tuo-bu-pai-x/)：

突破点：`拓扑排序。`

步骤：

1. 将组别为-1的项目都创建一个新组；
2. 遍历beforeItems\[i]\[j]数组；
3. 如果i和j属于同组，则确定组内优先级关系；
4. 若不同组，则确定小组间优先级关系；
5. 对每个组内拓扑排序；
6. 对不同组拓扑排序。

代码：

```c++
class Solution {
public:
  //拓扑排序的节点结构体声明
struct tpnod {
  //组外的优先级比该节点小的节点索引，维护不同的小组排序后的优先级关系
	vector<int>next1;
  //组内的优先级比该节点小的节点索引，维护同一小组的任务排序后的优先级关系
	vector<int>ingnext;
  //不同组间的在完成该节点之前需要完成的任务数
	int deg = 0;
  //组内的在完成该节点之前需要完成的任务数
	int igdeg = 0;
};
<<<<<<< HEAD
  
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
tpnod nos[30001];
//小组的数组，每个单元都是一个小组，可能不只m个，因为新创建了一些小组，但一定不会超过30000；
tpnod itogroup[30001];
//维护同一个组的项目
vector<int>grouptoi[30001];
//维护同一组的不同项目之间的顺序
vector<int>ingroup[30001];

    vector<int> sortItems(int n, int m, vector<int>& group, vector<vector<int>>& beforeItems) {
  //numOfG为包括创建的新组的组数
	int numOfG = m;
	vector<int>res;
	for (int i = 0; i < group.size(); i++) {
		if (group[i] != -1)
			grouptoi[group[i]].push_back(i);
		//否则创建新组
    else {
			grouptoi[numOfG].push_back(i);
			group[i] = numOfG;
			numOfG++;//创建后加一
		}
	}
	for (int i = 0; i < beforeItems.size(); i++) {
		for (int j = 0; j < beforeItems[i].size(); j++) {
      //在同一组就看作组内项目优先级关系
			if (group[beforeItems[i][j]] == group[i])
				nos[i].igdeg++, nos[beforeItems[i][j]].next1.push_back(i);
      //在不同组就看作组之间的优先级关系，因为同组的肯定是聚在一起的
			else itogroup[group[i]].deg++,
				itogroup[group[beforeItems[i][j]]].next1.push_back(group[i]);
		}
	}
<<<<<<< HEAD
  //确定不同小组组内项目优先级顺序     
=======
  //确定不同小组组内项目优先级顺序
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
	for (int i = 0; i < numOfG; i++) {
		queue<int>q;
		for (int j = 0; j < grouptoi[i].size(); j++) {
			if (nos[grouptoi[i][j]].igdeg == 0)
				q.push(grouptoi[i][j]);
		}
		int cnt2 = 0;
		while (!q.empty()) {
			cnt2++;
			int tp2 = q.front();
			ingroup[i].push_back(tp2);
			q.pop();
			for (int j = 0; j < nos[tp2].next1.size(); j++) {
				nos[nos[tp2].next1[j]].igdeg--;
        //在该节点之前的工作处理完了就把该节点放入队列
				if (nos[nos[tp2].next1[j]].igdeg == 0)
					q.push(nos[tp2].next1[j]);
			}
		}
<<<<<<< HEAD
    //判断是否矛盾 
=======
    //判断是否矛盾
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
		if (cnt2 != grouptoi[i].size()) {
			//res此时为空
      return res;
		}
	}
	queue<int>q;
	for (int i = 0; i < numOfG; i++)
		if (itogroup[i].deg == 0)
			q.push(i);
	int cnt3 = 0;
	int tp7;
	vector<int>grorder;
  //之前已经处理好了不同小组优先级关系，现在开始确定不同小组的顺序。
	while (!q.empty()) {
		tp7 = q.front();
		grorder.push_back(tp7);
		q.pop();
		cnt3++;
		for (int i = 0; i < itogroup[tp7].next1.size(); i++) {
			(itogroup[itogroup[tp7].next1[i]].deg)--;
			if (itogroup[itogroup[tp7].next1[i]].deg == 0)
				q.push(itogroup[tp7].next1[i]);
		}
	}
  //判断是否矛盾
	if (cnt3 != numOfG) {
    //res为空
		return res;
	}
	for (int i = 0; i < numOfG; i++) {
		for (int j = 0; j < ingroup[grorder[i]].size(); j++)
			res.push_back(ingroup[grorder[i]][j]);
	}
	return res;
  }
};
```
<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
