---
title: LeetCode题目总结-Array
date: 2020-09-06 21:09:19
categories:
- LeetCode
- Ch
tags:
- C++
- 算法
---

### 题目31:[下一个排列](https://leetcode-cn.com/problems/next-permutation)

**描述：**

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

<!--more-->

**[思路](https://leetcode-cn.com/problems/next-permutation/solution/c-4msti-jie-si-lu-jian-dan-4bu-jie-jue-by-jie-yi/)：**

突破点：`下一个更大排列的特性是什么。`

步骤（以[5,6,11,9,7,5,3,1]举例）：

1. 从尾部查找，直到找到当前元素大于前一元素，记录所在位置；

例：[5,6,11,9,7,5,3,1]，找到11大于6，记录位置2；

2. 从1.中的位置到数组尾部的子序列中，找到一个比前一位置的大且相差最小的数；

例：[5,6,11,9,7,5,3,1]，在[11,9,7,5,3,1]找到7，7是比6大且最接近6的，从尾部开始遍历，遍历到大于6的索引即可；

3. 交换2.中找到的数以及1.中确定的前一位置的数；

例：[5,6,11,9,7,5,3,1]，交换后变为[5,7,11,9,6,5,3,1]；

4. 将该位置到数组尾部的子序列进行升序排列，因为已经为降序（1.中确定的位置为首次部位降序的位置），所以首尾两两交换即可；

例：[5,7,11,9,6,5,3,1],交换后为[5,7,1,3,5,6,9,11]；

5. 另外，对于最大的排列，从小到大排列即可。

代码：

```C++
// 步骤2函数
int findMin(vector<int> nums, int i) {
  int pivotEle = nums[i-1];
  for (i = nums.size() - 1; i > -1; i--) {
    if (nums[i] > pivotEle) {
      break;
    }
  }
  return i;
}

// 步骤4函数，也可以用 reverse(nums.begin()+i, nums.end());实现
void swap(vector<int> &nums, int i) {
  int end = nums.size() - 1;
  while (i < end) {
    int temp = nums[i];
    nums[i] = nums[end];
    nums[end] = temp;
    i++;
    end--;
  }
}

class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int i;
        for(i = nums.size()-1; i>0; i--){
          	// 步骤1
            if(nums[i] > nums[i-1]) {
                int minIndex = findMin(nums, i);
              	//步骤3
                int minEle = nums[minIndex];
                nums[minIndex] = nums[i-1];
                nums[i-1] = minEle;
                swap(nums, i);
                break;
            }
        }
        if(0 == i) {
          	sort(nums.begin(), nums.end());
        }
    }
};
```

---

### 题目46:[全排列](https://leetcode-cn.com/problems/permutations)

**描述：**

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

[思路一](https://leetcode-cn.com/problems/permutations/solution/quan-pai-lie-by-leetcode-solution-2/)：

突破点：`回溯法。`

步骤（以[2, 5, 8, 9, 10]为例）：

1. 定义backtrack(first, ouput)函数，表示从左到右填到第first个位置，当前排列为ouput，进行递归；
2. 如果n==first，证明已经填完，结束递归；
3. 如果n>first，可通过标记数组标记已经填过的数，填入未标记的数字后，调用backtrack(first+1, output)；

4. 优化空间：将标记数组划分为左右两部分，左边已填过，右边未填过，动态维护。

例：[2, 5, 8, 9, 10]中已经填了[8, 9]，此时数组为[8, 9 | 2, 5, 10]，要填10，则交换2和10，数组变为[8, 9, 10 | 2, 5]。

代码：

```C++
class Solution {
public:
    void backtrack(vector<vector<int>>& res, vector<int>& output, int first, int len){
        if (first == len) {
          	// 关于emplace_back有专门的文章
            res.emplace_back(output);
            return;
        }

        for (int i = first; i < len; ++i) {
            // 动态维护数组
            swap(output[i], output[first]);
            // 继续递归填下一个数
            backtrack(res, output, first + 1, len);
            // 撤销操作
            swap(output[i], output[first]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int> > res;
        backtrack(res, nums, 0, (int)nums.size());
        return res;
    }
};

```

**[思路二](https://leetcode-cn.com/problems/permutations/solution/c-ru-ci-jian-ji-qie-jian-dan-de-di-gui-ni-ye-neng-/)**：（注意输出顺序与题目要求不符）

突破点：`递归。`

步骤（以[1, 2, 3]为例）：

1. 数组中每一个元素与最后一个元素互换；

例：[1, 2, 3]得到：[3, 2, 1]、[1, 3, 2]、[1, 2, 3]；

2. 将最后一个元素进行保存，考虑剩余元素，对剩余元素进行递归全排列求解；

例：对1.中[3, 2, 1]，递归求解[3, 2]得到[[3, 2], [2, 3]]；

3. 将2.中保存的最后元素加入子序列，得到结果；

例：对2.中，得到[[3, 2, 1], [2, 3, 1]]；

4. 继续循环完成剩余情况。

例：[1, 2, 3]剩余[1, 3, 2]和[1, 2, 3]。

代码：

```c++
class Solution {
public:
    vector<vector<int> > permute(vector<int>& nums) {
		vector<vector<int> > ans;

		if(1 == nums.size()) {
			ans.push_back(nums);
			return ans;
		} else {
			vector<vector<int> > tempAns;
			vector<int> ncp = nums;
      //步骤4
			for(int i = 0; i < nums.size(); i++) {
        //步骤1
				int temp = nums[i];
				nums[i] = nums[nums.size()-1];
				nums[nums.size()-1] = temp;
        //步骤2
				int end = nums[nums.size()-1];
				nums.pop_back();
				tempAns=permute(nums);
        //步骤3
				for (auto j : tempAns) {
        	j.push_back(end);
        	ans.push_back(j);
        }
				nums = ncp;
			}
			return ans;
    }
  }
};


```

---

### 题目79:[单词搜索](https://leetcode-cn.com/problems/word-search/)

**描述：**

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```

**提示：**

- `board` 和 `word` 中只包含大写和小写英文字母。
- `1 <= board.length <= 200`
- `1 <= board[i].length <= 200`
- `1 <= word.length <= 10^3`

[思路](https://leetcode-cn.com/problems/word-search/solution/tu-jie-di-gui-shen-du-you-xian-sou-suo-by-z1m/)：

突破点：`深度优先搜索。`

步骤（以ABCCEE为例）：

1. 采用暴力搜索找到第一个字符；

例：ABCCEE中的A；

2. 按照深度优先搜索寻找是否有匹配字符串，找到返回true，没有则寻找下一个第一字符；

例：如果没找到，继续寻找下一个A；

3. 为了避免重复，将搜索过的字符置为0。

代码：

```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if(0 == board.size()) {
          return false;
        }
        for (int i= 0; i < board.size(); i++) {
            for(int j = 0; j < board[0].size(); j++) {
                if (dfs(board, word, i, j, 0)){
                    return true;
                }
            }
        }
        return false;
    }

    bool dfs(vector<vector<char>>& board, string& word, int i,int j,int length){
        if (i >= board.size() || j >= board[0].size() || i < 0 || j < 0 || length >= word.size() || word[length] != board[i][j]) {
            return false;
        }
        if(length == word.size()-1 && word[length] == board[i][j]) {
            return true;
        }
        char temp = board[i][j];
        board[i][j] = '0';
        bool flag = dfs(board, word, i, j+1, length+1) || dfs(board, word, i, j-1, length+1) || dfs(board, word, i+1, j, length+1) || dfs(board, word, i-1, j, length+1);
      	// 标记过的点恢复原状，以便进行下一次搜索
        board[i][j] = temp;
        return flag;
    }
};


```

---

### 题目212:[单词搜索II](https://leetcode-cn.com/problems/word-search-ii/)

**描述：**

给定一个二维网格 board 和一个字典中的单词列表 words，找出所有同时在二维网格和字典中出现的单词。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母在一个单词中不允许被重复使用。

示例:

输入:
words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]

输出: ["eat","oath"]
说明:
你可以假设所有输入都由小写字母 a-z 组成。

提示:

你需要优化回溯算法以通过更大数据量的测试。你能否早点停止回溯？
如果当前单词不存在于所有单词的前缀中，则可以立即停止回溯。什么样的数据结构可以有效地执行这样的操作？散列表是否可行？为什么？ 前缀树如何？如果你想学习如何实现一个基本的前缀树，请先查看这个问题： 实现Trie（前缀树）。

[思路](https://leetcode-cn.com/problems/word-search-ii/solution/cqian-zhui-shu-ju-ta-ma-rong-yi-dong-by-chashao/)：

突破点：`前缀树。`

步骤：

1. 对于board使用DFS；
2. 使用前缀树，在递归遍历前缀树时，在当前字符不同时分开遍历。

代码：

```c++
struct Node {
    bool word;
    string str;
    unordered_map<char, Node*> words;
};
class Trie {
public:
    Trie() {
        root = new Node();
    }
    void insert(string word) {
        Node* p = root;
        for (char c: word) {
            if (p->words.find(c) == p->words.end()) {
                Node* t = new Node();
                p->words[c] = t;
            }
            p = p->words[c];
        }
      	// node对应的word，为了之后根据node来找到结果
        p->str = word;
        p->word = true;
    }
    void search(vector<string>& res, vector<vector<char>>& board) {
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[i].size(); j++) {
                help(res, board, root, i, j);
            }
        }
    }
    void help(vector<string>&res, vector<vector<char>>& board, Node* p, int x, int y) {
        if (p->word) {
          	// 其他方向就不会再把答案放进去了
            p->word = false;
            res.push_back(p->str);
            return;
        }
        if (x < 0 || x == board.size() || y < 0 || y == board[x].size()) return;
        if (p->words.find(board[x][y]) == p->words.end()) return;
      	// 此时的p是其他字符了
        p = p->words[board[x][y]];
        char cur = board[x][y];
        board[x][y] = '0';
        help(res, board, p, x+1, y);
        help(res, board, p, x-1, y);
        help(res, board, p, x, y+1);
        help(res, board, p, x, y-1);
        board[x][y] = cur;
    }

private:
    Node* root;
};
class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        Trie trie;
        vector<string> res;
        for (string& w: words) {
            trie.insert(w);
        }
        trie.search(res, board);
        return res;
    }
};

```

---

### 题目84:[柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram)

**描述：**

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

例，给定的高度为 [2,1,5,6,2,3]。

所能勾勒出的最大矩形面积为 10 个单位。

[思路]()：

突破点：`单调栈。`

步骤：

1. 对于每一个高度，利用单调栈获取向左和向右的边界；
2. 对每个高度求一次面积；
3. 遍历所有高度，求出最大面积。

代码：

```c++
int largestRectangleArea(vector<int>& heights) {
    int ans = 0;
    vector<int> monoStack;
    heights.insert(heights.begin(), 0);
    heights.push_back(0);
    for (int i = 0; i < heights.size(); i++) {
        while (!monoStack.empty() && heights[monoStack.back()] > heights[i]) {
            int cur = monoStack.back();
            monoStack.pop_back();
            int left = monoStack.back() + 1;
            int right = i - 1;
            ans = max(ans, (right - left + 1) * heights[cur]);
        }
        monoStack.push_back(i);
    }
    return ans;
}
```

---

### 题目85:[最大矩形](https://leetcode-cn.com/problems/maximal-rectangle/)

**描述：**

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

示例:

输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6

[思路](https://leetcode-cn.com/problems/maximal-rectangle/solution/dong-tai-gui-hua-by-leeyupeng-5/)：

突破点：`动态规划。`

步骤：

1. heights\[i\]\[j\]代表\[i, j]的高度；
2. dp\[i\]\[j\]\[p\]代表以\[i, j]为右下角，高度为k可以组成的面积。

代码：

```c++
class Solution {
public:
	int maximalRectangle(vector<vector<char> >& matrix) {
		int n = matrix.size();
		int m = 0;
		if (n > 0) {
      m = matrix[0].size();
    }
		vector<vector<int> > heights(n+1, vector<int>(m+1, 0));
		vector<vector<vector<int> > > dp(n+1, vector<vector<int> >(m+1, vector<int>(n+1, 0)));
		int ans = 0;
		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= m; j++) {
				if ('0' == matrix[i-1][j-1]) {
          continue;
        }
				heights[i][j] = heights[i-1][j] + 1;
				for (int k = 1; k <= heights[i][j]; k++) {
					dp[i][j][k] = dp[i][j-1][k] + k;
					ans = max(ans, dp[i][j][k]);
				}
			}
		}
		return ans;
	}
};
```

---

### 题目153:[寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

**描述：**

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

示例 1:

输入: [3,4,5,1,2]
输出: 1

[思路](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/er-fen-cha-zhao-wei-shi-yao-zuo-you-bu-dui-cheng-z/)：

突破点：`二分查找。`

代码：

```c++
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > nums[right]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return nums[left];
    }
};
```

---

### 题目154:[寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

**描述：**

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

注意数组中可能存在重复的元素。

示例 1：

输入: [1,3,5]
输出: 1
示例 2：

输入: [2,2,2,0,1]
输出: 0
说明：

这道题是 寻找旋转排序数组中的最小值 的延伸题目。
允许重复会影响算法的时间复杂度吗？会如何影响，为什么？

[思路](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/solution/zi-jie-ti-ku-154-kun-nan-xun-zhao-xuan-zhuan-pai-x/)：

突破点：`二分查找。`

代码：

```c++
class Solution {
public:
    int findMin(vector<int>& nums) {
        if(nums.empty()) return -1;
        if(1 == nums.size()) return nums[0];
        int p1 = 0, p2 = nums.size() - 1;
      	// 假如旋转了数组的前面0个元素（也就是没有旋转），我们直接返回numbers[p1]
        int mid = p1;
        while(nums[p1] >= nums[p2]) {
            if(1 == p2 - p1) {
                // 循环终止条件：当p2-p1=1时，p2所指元素为最小值
                mid = p2;
                break;
            }
          	// 二分法找中点
            mid = (p2 + p1) / 2;
            // 特殊情况：p1、mid、p2三处的元素的值一样，无法判断最小值在mid前面还是后面，就只能顺序查找了
            if(nums[p1] == nums[p2] && nums[p1] == nums[mid]) return findMin(nums, p1, p2);
            // 缩小范围，mid处值大于等于p1处值的话，说明最小值在mid处或mid后面，故将p1挪到mid处
            if(nums[mid] >= nums[p1]) p1 = mid;
            // 缩小范围，mid处值小于p1处值的话，说明最小值在mid处或mid前面，故将p2挪到mid处
            else p2 = mid;
        }
        return nums[mid];
    }

  	// 顺序查找
    int findMin(vector<int>& nums, int p1, int p2) {
        int res = nums[p1];
        for(int i=p1+1; i<=p2; ++i) {
            if(nums[i] < res) return nums[i];
        }
        return res;
    }
};
```
