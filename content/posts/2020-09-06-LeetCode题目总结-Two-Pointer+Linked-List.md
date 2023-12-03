---
title: LeetCode题目总结-Two Pointer+Linked List
date: 2020-09-06 23:33:19
categories: 
- LeetCode
tags:
- C++
- 算法
---

### 题目3:[无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

---

描述：

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

<!--more-->

示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

[思路一](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/wu-zhong-fu-zi-fu-de-zui-chang-zi-chuan-cshi-xian-/)：

突破点：`滑动窗口。`

步骤：

1. 设立指针a和指针b；
2. b指针向右伸缩，对于每个A\[b]判断是否之前出现过；
3. 若出现，则a指向出现过的未知的下一位置，更新右指针和最大长度。

代码：

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //s[start,end) 前面包含 后面不包含
        int start(0), end(0), length(0), result(0);
        int stringSize = int(s.size());
        while (end < stringSize) {
            char tmpChar = s[end];
            for (int index = start; index < end; index++) {
                if (tmpChar == s[index]) {
                    start = index + 1;
                    length = end - start;
                    break;
                }
            }

            end++;
            length++;
            result = max(result, length);
        }
        return result;
    }
};
```

[思路二](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/wu-zhong-fu-zi-fu-de-zui-chang-zi-chuan-cshi-xian-/)：

突破点：`hashMap。`

步骤：

1. 与思路一类似；
2. 在判断是否出现过时，使用hashmap优化时间。
3. b指针向右伸缩，对于每个A\[b]判断是否之前出现过；
4. 若出现，则a指向出现过的未知的下一位置，更新右指针和最大长度。

代码：

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //s[start,end) 前面包含 后面不包含
        int start(0), end(0), length(0), result(0);
        int sSize = int(s.size());
      
        unordered_map<char, int> hash;
      
        while (end < sSize) {
            char tmpChar = s[end];
            //仅当s[start,end) 中存在s[end]时更新start
            if (hash.find(tmpChar) != hash.end() && hash[tmpChar] >= start) {
                start = hash[tmpChar] + 1;
                length = end - start;
            }
            hash[tmpChar] = end;

            end++;
            length++;
            result = max(result, length);
        }
        return result;
    }
};
```

---

### 题目75:[颜色分类](https://leetcode-cn.com/problems/sort-colors/)

---

描述：

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:

输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
进阶：

一个直观的解决方案是使用计数排序的两趟扫描算法。
首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
你能想出一个仅使用常数空间的一趟扫描算法吗？

[思路](https://leetcode-cn.com/problems/sort-colors/solution/yan-se-fen-lei-by-leetcode/)：

突破点：`三指针。`

步骤：

1. 定义三个指针p0、p2、curr来追踪0、2的边界以及当前考虑的元素；
2. 初始化p0 = 0，p2 = n-1；
3. 当curr<=p2时，如果nums[curr] = 0，则交换curr和p0所指元素，并将curr和p0右移；
4. 如果nums[curr] = 2，则交换curr和p2所指元素，并将p2左移，注意此时为了将判断移过来的元素类型而不右移curr；
5. 如果nums[curr] = 1，则curr右移。

代码：

```c++
class Solution {
  public:
  /*
  荷兰三色旗问题解
  */
  void sortColors(vector<int>& nums) {
    // 对于所有 idx < p0 : nums[idx < p0] = 0
    // curr 是当前考虑元素的下标
    int p0 = 0, curr = 0;
    // 对于所有 idx > p2 : nums[idx > p2] = 2
    int p2 = nums.size() - 1;

    while (curr <= p2) {
      if (nums[curr] == 0) {
        swap(nums[curr++], nums[p0++]);
      }
      else if (nums[curr] == 2) {
        swap(nums[curr], nums[p2--]);
      }
      else curr++;
    }
  }
};
```

---

### 题目88:[合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

---

描述：

给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。


示例:

输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]

[思路](https://leetcode-cn.com/problems/merge-sorted-array/solution/88-by-ikaruga/):

突破点：`归并排序思想。`

步骤：

1. 获取nums1数组的尾部指针；
2. 从两数组尾部开始，交换较大值和nums1尾部位置。

代码：

```c++
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int i = nums1.size() - 1;
    m--;
    n--;
    while (n >= 0) {
        while (m >= 0 && nums1[m] > nums2[n]) {
            swap(nums1[i--], nums1[m--]);
        }
        swap(nums1[i--], nums2[n--]);
    }
}
```

---

### 题目125:[验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

---

描述：
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**

```
输入: "race a car"
输出: false
```

[思路](https://leetcode-cn.com/problems/valid-palindrome/solution/cdai-ma-by-orange-32-6/)：

突破点：`首尾指针比较。`

步骤：

1. 一个指针指向头部，一个指针指向尾部；
2. 分别从首尾开始比较，数字全部转化为小写比较；
3. 如果有不同，则返回false。

代码：

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        for (int i = 0, j = s.length() - 1; i < j; i ++, j --) {
            while(i < j && !isalnum(s[i])) i ++;
            while(i < j && !isalnum(s[j])) j --;
            if(tolower(s[i]) != tolower(s[j])) return false;
        }
        return true;
    }
};
```

---

### 题目76:[最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)

---

描述：

给你一个字符串 S、一个字符串 T 。请你设计一种算法，可以在 O(n) 的时间复杂度内，从字符串 S 里面找出：包含 T 所有字符的最小子串。

示例：

输入：S = "ADOBECODEBANC", T = "ABC"
输出："BANC"


提示：

如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。

[思路](https://leetcode-cn.com/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-by-leetcode-solution/)：

突破点：`滑动窗口。`

步骤：

1. 声明两个指针left和right，right用于延伸窗口，left用于收缩窗口；
2. 首先移动right使得窗口内包含t所有字符；
3. 然后收缩left且保证收缩过程中t仍在窗口内；
4. 使用哈希表动态维护窗口中字符数以及t中字符数。

代码：

```c++
class Solution {
public:
    unordered_map <char, int> ori, cnt;

  	// 步骤4
    bool check() {
        for (const auto &p: ori) {
            if (cnt[p.first] < p.second) {
                return false;
            }
        }
        return true;
    }

  	// 滑窗
    string minWindow(string s, string t) {
        for (const auto &c: t) {
            ++ori[c];
        }

      	// 步骤1
        int l = 0, r = -1;
        int len = INT_MAX, ansL = -1, ansR = -1;

      	// 步骤2
        while (r < int(s.size())) {
            if (ori.find(s[++r]) != ori.end()) {
                ++cnt[s[r]];
            }
          	// 步骤3
            while (check() && l <= r) {
                if (r - l + 1 < len) {
                    len = r - l + 1;
                    ansL = l;
                }
                if (ori.find(s[l]) != ori.end()) {
                    --cnt[s[l]];
                }
                ++l;
            }
        }

        return ansL == -1 ? string() : s.substr(ansL, len);
    }
};
```

---

### 题目206:[反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

---

描述：

反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

[思路一](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-shuang-zhi-zhen-di-gui-yao-mo-/)：

突破点：`双指针。`

步骤：

1. 定义一前一后两个指针pre和cur；
2. 每次让pre的next指向cur，实现局部反转；
3. 局部反转后，两个指针同时前移一位，直到pre到达链表结尾。

代码：

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = nullptr, *pre = head;
        while (nullptr != pre) {
            ListNode* t = pre->next;
            pre->next = cur;
            cur = pre;
            pre = t;
        }
        return cur;
    }
};
```

[思路二](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-shuang-zhi-zhen-di-gui-yao-mo-/)：

突破点：`递归。`

步骤：

1. 一直递归到链表最后一个节点；
2. 每次返回时，让当前节点的下一节点的next指针指向当前节点；
3. 让当前节点的next指针指向nullptr；
4. 递归函数全部出栈后，反转完成。

代码：

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (nullptr == head || nullptr == head->next) {
          return head;
        }
      	ListNode* ret = reverseList(head->next);
      	head->next->next = head;
     	 	head->next = nullptr;
      	return ret;
    }
};
```

---

### 题目21:[合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

---

描述：

将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

[思路](https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/)：

突破点：`递归。`

步骤：

1. 递归时，首先比较两个输入头节点的大小；
2. 若list1小于list2的头节点，则尾部添加list1后继续递归；
3. 若list1大于list2的头节点，则尾部添加list2后继续递归。

代码：

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (nullptr == l1) {
            return l2;
        } else if (nullptr == l2) {
            return l1;
        } else if (l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```

---

### 题目23:[合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

---

描述：

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

示例 1：

输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
示例 2：

输入：lists = []
输出：[]
示例 3：

输入：lists = [[]]
输出：[]


提示：

k == lists.length
0 <= k <= 10^4
0 <= lists[i].length <= 500
-10^4 <= lists[i][j] <= 10^4
lists[i] 按 升序 排列
lists[i].length 的总和不超过 10^4

[思路一](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/he-bing-kge-pai-xu-lian-biao-by-leetcode-solutio-2/)：

突破点：`分治合并。`

步骤：

1. 将k个链表配对，并两两合并；
2. 重复1.中过程，直到得到最终链表。

代码：

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode *a, ListNode *b) {
        if ((!a) || (!b)) return a ? a : b;
        ListNode head, *tail = &head, *aPtr = a, *bPtr = b;
        while (aPtr && bPtr) {
            if (aPtr->val < bPtr->val) {
                tail->next = aPtr; 
              	aPtr = aPtr->next;
            } else {
                tail->next = bPtr; 
              	bPtr = bPtr->next;
            }
            tail = tail->next;
        }
        tail->next = (aPtr ? aPtr : bPtr);
        return head.next;
    }

    ListNode* merge(vector <ListNode*> &lists, int l, int r) {
        if (l == r) return lists[l];
        if (l > r) return nullptr;
        int mid = (l + r) >> 1;
        return mergeTwoLists(merge(lists, l, mid), merge(lists, mid + 1, r));
    }

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        return merge(lists, 0, lists.size() - 1);
    }
};
```

[思路二](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/he-bing-kge-pai-xu-lian-biao-by-leetcode-solutio-2/)：

突破点：`优先队列。`

步骤：

1. 维护当前每个链表没有别合并的元素最前面的一个；
2. 每次在1.中选取val值最小的元素合并到result中；
3. 使用优先队列进行优化。

代码：

```c++
class Solution {
public:
    struct Status {
        int val;
        ListNode *ptr;
        bool operator < (const Status &rhs) const {
            return val > rhs.val;
        }
    };

    priority_queue <Status> q;

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        for (auto node: lists) {
            if (node) q.push({node->val, node});
        }
        ListNode head, *tail = &head;
        while (!q.empty()) {
            auto f = q.top(); q.pop();
            tail->next = f.ptr; 
            tail = tail->next;
            if (f.ptr->next) q.push({f.ptr->next->val, f.ptr->next});
        }
        return head.next;
    }
};
```

