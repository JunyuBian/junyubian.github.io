---
title: LeetCode题目总结-DP+Greedy
date: 2020-09-11 11:52:19
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

### 题目5:[最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

<!--more-->

示例 2：

输入: "cbbd"
输出: "bb"

[思路一](https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zui-chang-hui-wen-zi-chuan-c-by-gpe3dbjds1/)：（时间超限）

突破点：`反转字符串的公共子串。`

步骤：

1. 将输入的字符串反转；
2. 求两者的公共子串；
3. 判断该子串是否为所需的最长回文子串。

代码：

```c++
class Solution {
public:
    string longestPalindrome(string s) {
      	//大小为1的字符串必为回文串
        if(s.length() == 1) return s;
        string rev = s;
        string res;
        std::reverse(rev.begin(),rev.end());
        if(rev == s) return s;
	      //存放回文子串的长度
        int len = 0;
	      //查找s与rev的最长公共子串
        for(int i=0; i<s.length(); i++) {
          	//存放待验证子串
            string temp;
            for(int j=i; j<s.length(); j++) {
                temp = temp+s[j];
                if(len >= temp.length()) {
                    continue;
                } else if(rev.find(temp) != -1) {//在rev中找到temp
                    string q = temp;//q用来验证temp是否是回文子串
                    std::reverse(q.begin(),q.end());
                    if(q == temp) {
                        len = temp.length();
                        res = temp;
                    }
                } else {
                  break;
                }
            }
            temp="";
        }
        return res;
    }
};
```

[思路二](https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zui-chang-hui-wen-zi-chuan-by-leetcode-solution/)：

突破点：`动态规划。`

步骤：

1. P(i, j) 表示字符串s的第i到j个字母组成的子串是否为回文串；
2. 状态转移方程：`P(i, j) = P(i+1, j-1)$\and$ (Si == Sj)`，即只有当s\[i+1:j-1\]是回文串，并且s的第i和j个字母相同时，s\[i:j\]才会是回文串；
3. 边界条件：当长度为1时，一定为回文串，当长度为2时，若两字母相同，则为回文串。

代码：

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<int> > dp(n, vector<int>(n));
        string ans;
<<<<<<< HEAD
      
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
        for (int l = 0; l < n; ++l) {
            for (int i = 0; i + l < n; ++i) {
                int j = i + l;
                if (l == 0) {
                    dp[i][j] = 1;
                } else if (l == 1) {
                    dp[i][j] = (s[i] == s[j]);
                } else {
                    dp[i][j] = (s[i] == s[j] && dp[i + 1][j - 1]);
                }
                if (dp[i][j] && l + 1 > ans.size()) {
                    ans = s.substr(i, l + 1);
                }
            }
        }
        return ans;
    }
};
```

---

### 题目139:[ 单词拆分](https://leetcode-cn.com/problems/word-break/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。
示例 1：

输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
示例 2：

输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
示例 3：

输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false

[思路](https://leetcode-cn.com/problems/word-break/solution/dan-ci-chai-fen-by-leetcode-solution/)：

突破点：`动态规划。`

步骤：

1. dp\[i]表示前i个字符组成的字符串s\[0...i-1]是否能够被空格拆分成若干个字典中出现的单词；
2. 对于转移方程，我们需要枚举s\[0...i-1]中的分割点j，看s\[0...j-1]组成的字符串s1和s\[j...i-1]组成的字符串s2是否都合法，如果均合法，则s1s2拼成的字符串也合法：`dp[i] = dp[j]&&check(s[j...i-1])`；
3. 可通过哈希表快速判断字符串是否在给定的字符串列表里，也可以做简单剪枝，当分割点j到i的长度大于字典中最大单词长度，则返回false。

代码：

```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        auto wordDictSet = unordered_set <string> ();
        for (auto word: wordDict) {
            wordDictSet.insert(word);
        }

        auto dp = vector <bool> (s.size() + 1);
        dp[0] = true;
        for (int i = 1; i <= s.size(); ++i) {
            for (int j = 0; j < i; ++j) {
                if (dp[j] && wordDictSet.find(s.substr(j, i - j)) != wordDictSet.end()) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.size()];
    }
};
```

---

### 题目140:[单词拆分 II](https://leetcode-cn.com/problems/word-break-ii/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，在字符串中增加空格来构建一个句子，使得句子中所有的单词都在词典中。返回所有这些可能的句子。

说明：

分隔时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。
示例 1：

输入:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
输出:
[
  "cats and dog",
  "cat sand dog"
]
示例 2：

输入:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
输出:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
解释: 注意你可以重复使用字典中的单词。
示例 3：

输入:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
输出:
[]

[思路](https://leetcode-cn.com/problems/word-break-ii/solution/140-by-ikaruga/)：

突破点：`动态规划。`

步骤：

1. 首先判断能否拆分；
2. 定义vector\<vector\<string> > dp(s.size() + 1, vector\<string>())；
3. 假设从开始到i-1个字符是如字典匹配的一个词，则第i个字符是一个新词的开头字母；
4. 添加这个词到dp\[i]中；
5. 从第i个字符开始，如果再匹配到一个词，把dp\[i]中的每个词加上空格，再加上新词，添加到后面的dp\[j]中；
6. dp\[i]表示第i个字符前的所有拆分情况。

代码：

```c++
class Solution {
public:
	vector<string> wordBreak(string s, vector<string>& wordDict) {
		if (!wordBreak_139(s, wordDict)) return {};
		size_t validEnd = 0;
		vector<vector<string> > dp(s.size() + 1, vector<string>());

		for (size_t i = 0; i < s.size(); i++) {
			if (i == validEnd + 1) return {};
			if (i != 0 && dp[i].empty()) continue;
			for (auto& word : wordDict) {
				size_t newEnd = i + word.size();
				if (newEnd > s.size()) continue;
				if (memcmp(&s[i], &word[0], word.size()) != 0) continue;
				validEnd = max(validEnd, newEnd);
				if (i == 0) {
					dp[newEnd].push_back(word);
					continue;
				}
				for (auto& d : dp[i]) {
					dp[newEnd].push_back(d + " " + word);
				}
			}
		}
		return dp.back();
	}

	bool wordBreak_139(string& s, vector<string>& wordDict){
		size_t validEnd = 0;
		vector<bool> dp(s.size() + 1, false);
		dp[0] = true;
		for (size_t i = 0; i < s.size(); i++) {
			if (i == validEnd + 1) return false;
			if (!dp[i]) continue;
			for (auto& word : wordDict) {
				size_t newEnd = i + word.size();
				if (newEnd > s.size()) continue;
				if (memcmp(&s[i], &word[0], word.size()) == 0) {
					dp[newEnd] = true;
					validEnd = max(validEnd, newEnd);
				}
			}
		}
		return dp.back();
	}
};
```

---

### 题目62:[不同路径](https://leetcode-cn.com/problems/unique-paths/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

示例 1:

输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
示例 2:

输入: m = 7, n = 3
输出: 28

<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
提示：

1 <= m, n <= 100
题目数据保证答案小于等于 2 * 10 ^ 9

[思路](https://leetcode-cn.com/problems/unique-paths/solution/kan-liao-jue-dui-dong-de-dong-tai-gui-hua-by-stree/)：

突破点：`动态规划。`

步骤：

1. 状态方程：dp\[i]\[j]；
2. 状态转移方程：`dp[i][j] = dp[i-1][j] +dp[i][j-1]`；
3. 边界条件：dp\[0]\[j]全为1，dp\[i]\[0]全为1。

代码：

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int> > dp(m+1, vector<int>(n+1));
        dp[0][1] = 1;

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }

        return dp[m][n];
    }
};
```

---

### 题目63:[不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

示例 1:

输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右

[思路](https://leetcode-cn.com/problems/unique-paths-ii/solution/dong-tai-gui-hua-by-acw_wangdh15-6/)：

突破点：`动态规划。`

步骤：

1. 状态方程：dp\[i]\[j]表示到i, j的方法数；
2. 状态转移方程：
   1. 如果这个位置有障碍，则dp\[i]\[j] = 0；
   2. 如果没有障碍，则`dp\[i]\[j] = dp\[i-1]\[j] + dp\[i]\[j-1]`。

代码：

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& ob) {
        int n = ob.size();
        if (n == 0) return 0;
        if (ob[0][0] == 1) return 0;
        int m = ob[0].size();
        vector<vector<int> > dp(n + 1, vector<int>(m + 1, 0));
<<<<<<< HEAD
      
=======

>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
        for (int i = 1; i <= n; i ++) {
            for (int j = 1; j <= m; j ++) {
                if (i == 1 && j == 1) dp[i][j] = 1;
                else {
                    if (ob[i-1][j-1] == 1) dp[i][j] = 0;
                    else dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[n][m];
    }
};
```

---

### 题目121:[买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

示例 1:

输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
示例 2:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

[思路](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/gu-piao-wen-ti-python3-c-by-z1m/)：

突破点：`动态规划。`

步骤：

1. 状态方程：dp\[i]表示前i天的最大利润；
2. 状态转移方程：`dp[i] = max(dp[i-1], prices[i] - minPrice)`。

代码：

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n == 0) return 0; // 边界条件
        int minprice = prices[0];
        vector<int> dp (n, 0);

        for (int i = 1; i < n; i++){
            minprice = min(minprice, prices[i]);
            dp[i] = max(dp[i - 1], prices[i] - minprice);
        }
        return dp[n - 1];
    }
};
```

---

### 题目122:[买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

<<<<<<< HEAD
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。 
=======
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

示例 1:

输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
示例 2:

输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
提示：

1 <= prices.length <= 3 * 10 ^ 4
0 <= prices[i] <= 10 ^ 4

[思路](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/mai-mai-gu-piao-de-zui-jia-shi-ji-ii-tan-xin-suan-/)：

突破点：`动态规划。`

步骤：

1. 状态方程：dp\[i]\[0]表示第i天不持有股票时的利益，dp\[i]\[1]表示第i天持有股票时的利益；
2. 状态转移方程：`dp[i][0] = max(dp[i-1][0], dp[i-1][1] + prices[i])`，`dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i])`。

代码：

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // 动态规划解法
        // 0.初始判断
        if(prices.empty()) return 0;
        int dp[prices.size()][2];
        // 1.初始状态
        dp[0][0] = 0;
        dp[0][1] = -prices[0];

        // 2.状态转移
        for(int i = 1; i<prices.size();i++){
            // 3.状态转移方程
            dp[i][0] = max(dp[i-1][0], dp[i-1][1] + prices[i]);
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i]);
        }
        return dp[prices.size()-1][0];
    }
};
```

---

### 题目55:[跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

示例 1:

输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
示例 2:

输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。

[思路](https://leetcode-cn.com/problems/jump-game/solution/55-by-ikaruga/)：

突破点：`贪心。`

步骤：

1. 对于可以作为起跳点的格子都做一次尝试；
2. 更新能跳到的最远距离；
3. 如果能调到末尾，则成功。

代码：

```c++
bool canJump(vector<int>& nums) {
	int k = 0;
	for (int i = 0; i < nums.size(); i++) {
		if (i > k) return false;
		k = max(k, i + nums[i]);
	}
	return true;
}
```

---

### 题目45:[跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

<<<<<<< HEAD
---

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
描述：
给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

**示例:**

```
输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**说明:**

假设你总是可以到达数组的最后一个位置。

[思路](https://leetcode-cn.com/problems/jump-game-ii/solution/45-by-ikaruga/)：

突破点：`贪心算法。`

步骤：

1. 每一次跳跃，更新下一次起跳点的范围；
2. 在新的范围内，更新能跳到的最远距离；
3. 记录跳跃次数，如果能到终点，则返回结果。

代码：

```c++
int jump(vector<int>& nums) {
    int ans = 0;
    int end = 0;
    int maxPos = 0;
    for (int i = 0; i < nums.size() - 1; i++) {
        maxPos = max(nums[i] + i, maxPos);
        if (i == end) {
            end = maxPos;
            ans++;
        }
    }
    return ans;
}
```
<<<<<<< HEAD

=======
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
