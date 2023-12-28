---
title: LeetCode题目总结-Heap+Stack
date: 2020-09-09 12:32:19
categories: 
- LeetCode
tags:
- C++
- 算法
- ch
---

### 题目20:[有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

---

描述：

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

输入: "()"
输出: true
示例 2:

输入: "()[]{}"
输出: true
示例 3:

输入: "(]"
输出: false
示例 4:

输入: "([)]"
输出: false
示例 5:

输入: "{[]}"
输出: true

[思路](https://leetcode-cn.com/problems/valid-parentheses/solution/zhu-bu-fen-xi-tu-jie-zhan-zhan-shi-zui-biao-zhun-d/)：

突破点：`使用栈模拟删除过程。`

步骤：

1. 使用栈进行存储；
2. 当匹配到最小的括号对时，将这一对从栈中删除；
3. 如果最后栈为空，则为有效。

代码：

```c++
class Solution {
public:
    bool isValid(string s) {
        unordered_map<char,int> m{{'(',1},{'[',2},{'{',3},
                                {')',4},{']',5},{'}',6}};
        stack<char> st;
        bool isTrue = true;
        for(char c:s){
            int flag = m[c];
            if(flag>=1 && flag<=3) {
              st.push(c);
            } else if(!st.empty() && m[st.top()]==flag-3) {
              st.pop();
            } else {
              isTrue = false;
              break;
            }
        }
        if(!st.empty()) {
          isTrue = false;
        }
        return isTrue;
    }
};
```

---

### 题目42:[接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

---

描述：

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

示例:

输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6

[思路一](https://leetcode-cn.com/problems/trapping-rain-water/solution/jie-yu-shui-by-leetcode/)：

突破点：`使用栈进行遍历。`

步骤：

1. 使用栈来跟踪可能储水的最长条形块；
2. 如果当前条形块小于或等于栈顶条形块，则将条形块入栈；
3. 如果当前条形块大于栈顶条形块，则暗处栈顶元素，并累加到结果中。

代码：

```c++
int trap(vector<int>& height) {
    int ans = 0, current = 0;
    stack<int> st;
    while (current < height.size()) {
        while (!st.empty() && height[current] > height[st.top()]) {
            int top = st.top();
            st.pop();
            if (st.empty())
                break;
            int distance = current - st.top() - 1;
            int bounded_height = min(height[current], height[st.top()]) - height[top];
            ans += distance * bounded_height;
        }
        st.push(current++);
    }
    return ans;
}
```

[思路二](https://leetcode-cn.com/problems/trapping-rain-water/solution/jie-yu-shui-by-leetcode/)：

突破点：`使用双指针。`

步骤：

1. 使用双指针；
2. 分别从左和右，更新left_max和right_max；
3. 当发现有小值出现，则累加差值到结果中。

代码：

```c++
int trap(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int ans = 0;
    int left_max = 0, right_max = 0;
    while (left < right) {
        if (height[left] < height[right]) {
            height[left] >= left_max ? (left_max = height[left]) : ans += (left_max - height[left]);
            ++left;
        } else {
            height[right] >= right_max ? (right_max = height[right]) : ans += (right_max - height[right]);
            --right;
        }
    }
    return ans;
}
```

---

### 题目71:[简化路径](https://leetcode-cn.com/problems/simplify-path/)

---

描述：

以 Unix 风格给出一个文件的绝对路径，你需要简化它。或者换句话说，将其转换为规范路径。

在 Unix 风格的文件系统中，一个点（.）表示当前目录本身；此外，两个点 （..） 表示将目录切换到上一级（指向父目录）；两者都可以是复杂相对路径的组成部分。更多信息请参阅：Linux / Unix中的绝对路径 vs 相对路径

请注意，返回的规范路径必须始终以斜杠 / 开头，并且两个目录名之间必须只有一个斜杠 /。最后一个目录名（如果存在）不能以 / 结尾。此外，规范路径必须是表示绝对路径的最短字符串。

示例 1：

输入："/home/"
输出："/home"
解释：注意，最后一个目录名后面没有斜杠。
示例 2：

输入："/../"
输出："/"
解释：从根目录向上一级是不可行的，因为根是你可以到达的最高级。
示例 3：

输入："/home//foo/"
输出："/home/foo"
解释：在规范路径中，多个连续斜杠需要用一个斜杠替换。
示例 4：

输入："/a/./b/../../c/"
输出："/c"
示例 5：

输入："/a/../../b/../c//.//"
输出："/c"
示例 6：

输入："/a//b////c/d//././/.."
输出："/a/b/c"

[思路一](https://leetcode-cn.com/problems/simplify-path/solution/c-zhan-xian-li-jie-ti-mu-ba-by-zuo-10/)：

突破点：`栈。`

步骤：

1. 需要处理三种情况：
   1. 保证路径以`/`进行分割；
   2. 遇到`..`，切换为上一级目录；
   3. 路径末尾没有`/`；
2. 使用栈进行存储和遍历处理。

代码：

```c++
class Solution {
public:
    string simplifyPath(string path) {
        path += "/";
        stack<string> st;
        string dir;
        for (auto c : path) {
            // 以 / 为分隔符
            if (c == '/') {
                // 切换上一集目录
                if (dir == ".." && !st.empty()) {
                    st.pop();
                } 
                // 上一个 '/' 到 下一个 '/'
                else if (dir != ".." && dir != "." && !dir.empty()) {
                    st.push(dir);
                }
                dir.clear();
            } else {
                dir += c;
            }
        }

        // 遍历栈
        string result;
        while (!st.empty()) {
            string s = st.top();
            st.pop();
            result = "/" + s + result;
        }
        if(result.empty()) result = "/";
        return result;
    }
};
```

[思路二](https://leetcode-cn.com/problems/simplify-path/solution/yong-you-xian-zhuang-tai-ji-de-si-xiang-lai-jie-zh/)：

突破点：`状态机。`

步骤：

1. 分为四种状态：
   1. 前面是一个正常的字符
      * 遇到`/`，则插入结果字符串中，并转至状态2；
      * 遇到`.`，则转到状态2；
      * 遇到一个正常字符，则插入结果字符串；
   2. 前面是一个`/`
      * 遇到`/`，直接跳过；
      * 遇到`.`，转到状态3；
      * 遇到一个正常字符，则插入结果字符串，并转到状态1；
   3. 前面是一个`.`
      * 遇到`/`，转到状态2；
      * 遇到`.`，转到状态4；
      * 遇到一个正常字符，插入`.`和这个字符，并转到状态1；
   4. 前面是`..`
      * 遇到`/`，则回溯删除到前面一个`/`；
      * 其余情况则插入一个`..`和当前字符，并转到状态1。

代码：

```c++
class Solution {
public:
    string simplifyPath(string path) {
        string res;
        
        // some flag to kepp state.
        int state = 0;  // 0: last char is [char]
                        // 1: last char is '/'
                        // 2: last char is '.'
                        // 3: last char is ".."
        
        if (path.size() != 0 && path[path.size()-1]!='/') path.push_back('/');
        
        int len = path.size();
        for(int i = 0; i < len; i++) {
            char c = path[i];
            
            if (state == 0) {
                if (c == '/') { res.push_back('/'); state = 1; }
                else if (c == '.') state = 2;
                else res.push_back(c);
            } else if (state == 1) {
                if (c == '/') {}
                else if (c == '.') { state = 2; }
                else {
                    res.push_back(c); state = 0;
                }
            } else if (state == 2) {
                if (c == '/') state = 1;
                else if (c == '.') {
                    // '..'
                    state = 3;
                } else {
                    res.push_back('.'); res.push_back(c); state = 0;
                }
            } else if (state == 3) {
                if (c == '/') {
                    // go back
                    res.pop_back(); // pop '/'
                    while(res.size() != 0 && *res.rbegin() != '/') {
                        res.pop_back(); // pop anthing until '/'
                    }
                    if (res.size() == 0) res.push_back('/');
                    state = 1;
                } else {
                    res.push_back('.'); 
                    res.push_back('.');
                    res.push_back(c);
                    state = 0;
                }
            }
            //cout << state << " " << c << " " << res <<  endl;
        }
        
        if ((state == 1 && res.size() != 1)) res.pop_back();
        return res;
    }
};
```

---

### 题目225:[ 用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

---

描述：

使用队列实现栈的下列操作：

push(x) -- 元素 x 入栈
pop() -- 移除栈顶元素
top() -- 获取栈顶元素
empty() -- 返回栈是否为空
注意:

你只能使用队列的基本操作-- 也就是 push to back, peek/pop from front, size, 和 is empty 这些操作是合法的。
你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。
你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。

[思路一](https://leetcode-cn.com/problems/implement-stack-using-queues/solution/yong-dui-lie-shi-xian-zhan-c-dan-dui-lie-ru-zhan-o/)：

突破点：`单队列。`

步骤：

1. 维护队列使队头对应栈顶，队尾对应栈底；
2. 在每次在队尾加入元素后，将原本的队列中的元素从头部取出，放入队尾，保证1的性质。

代码：

```c++
class MyStack {
public:
    /** Initialize your data structure here. */
    MyStack() = default;
    
    /** Push element x onto stack. */
    void push(int x) {
        que.push(x);
        int n = que.size();
        for (int i = 0; i + 1 < n; i++) {
            que.push(que.front());
            que.pop();
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int val = top();
        que.pop();
        return val;
    }
    
    /** Get the top element. */
    int top() {
        return que.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return que.empty();
    }

private:
    queue<int> que;
};
```

[思路二](https://leetcode-cn.com/problems/implement-stack-using-queues/solution/225-yong-dui-lie-shi-xian-zhan-liang-ge-dui-lie-sh/)：

突破点：`双队列。`

步骤：

1. 创建第二个辅助队列；
2. 第一个队列为主要的取值队列，第二个队列在pop操作时，作为拷贝辅助。

代码：

```c++
class MyStack {
public:
    queue<int> que1;
    queue<int> que2; // 辅助队列
    /** Initialize your data structure here. */
    MyStack() {

    }

    /** Push element x onto stack. */
    void push(int x) {
        que1.push(x);
    }

    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int size = que1.size();
        size--;
      	// 将que1 导入que2，但要留下最后一个元素
        while (size--) { 
            que2.push(que1.front());
            que1.pop();
        }

      	// 留下的最后一个元素就是我们要返回的值
        int result = que1.front(); 
        que1.pop();
      	// 再将que2赋值给que1
        que1 = que2; 
      	// 清空que2
        while(!que2.empty()) { 
            que2.pop();
        }
        return result;
    }

    /** Get the top element. */
    int top() {
        return que1.back();
    }

    /** Returns whether the stack is empty. */
    bool empty() {
        return que1.empty();
    }
};
```

---

### 题目232:[用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

---

描述：

使用栈实现队列的下列操作：

push(x) -- 将一个元素放入队列的尾部。
pop() -- 从队列首部移除元素。
peek() -- 返回队列首部的元素。
empty() -- 返回队列是否为空。


示例:

MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // 返回 1
queue.pop();   // 返回 1
queue.empty(); // 返回 false


说明:

你只能使用标准的栈操作 -- 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。
假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）。

[思路](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/232-yong-zhan-shi-xian-dui-lie-liang-ge-zhan-lai-m/)：

突破点：`两个栈实现队列。`

步骤：

1. 使用两个栈，一个作为输出，一个存储输入值；
2. 当需要pop时，判断输入栈是否为空；
3. 若为空，导入全部输入栈数据并pop；
4. 若不为空，直接pop（因为在peek查看元素之后，会push进输出栈）。

代码：

```c++
class MyQueue {
public:
    stack<int> stIn;
    stack<int> stOut;
    /** Initialize your data structure here. */
    MyQueue() {

    }
    /** Push element x to the back of queue. */
    void push(int x) {
        stIn.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        //只有当stOut为空的时候，再从stIn里导入数据（导入stIn全部数据）
        if (stOut.empty()) {
            // 从stIn导入数据直到stIn为空
            while(!stIn.empty()) {
                stOut.push(stIn.top());
                stIn.pop();
            }
        }
        int result = stOut.top();
        stOut.pop();
        return result;
    }

    /** Get the front element. */
    int peek() {
        int res = this->pop(); // 直接使用已有的pop函数
        stOut.push(res); // 因为pop函数弹出了元素res，所以再添加回去
        return res;
    }

    /** Returns whether the queue is empty. */
    bool empty() {
        return stIn.empty() && stOut.empty();
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

[思路一](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/c-you-xian-dui-lie-liang-liang-he-bing-fen-zhi-he-/)：

突破点：`优先队列。`

步骤：

1. 建立优先队列，使得每个链表头部元素入队；
2. 弹出后，将链表下一个元素入队。

代码：

```c++
class Solution {
public:
    // 小根堆的回调函数
    struct cmp{  
       bool operator()(ListNode *a,ListNode *b){
          return a->val > b->val;
       }
    };

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, cmp> pri_queue;
        // 建立大小为k的小根堆
        for(auto elem : lists){
            if(elem) pri_queue.push(elem);
        }
        // 可以使用哑节点/哨兵节点
        ListNode dummy(-1);
        ListNode* p = &dummy;
        // 开始出队
        while(!pri_queue.empty()){
            ListNode* top = pri_queue.top(); pri_queue.pop();
            p->next = top; p = top;
            if(top->next) pri_queue.push(top->next);
        }
        return dummy.next;  
    }
};
```

[思路二](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/c-you-xian-dui-lie-liang-liang-he-bing-fen-zhi-he-/)：

突破点：`两两合并。`

步骤：

1. 从头开始，两两合并链表。

代码：

```c++
class Solution {
public:
    // 合并两个有序链表
    ListNode* merge(ListNode* p1, ListNode* p2){
        if(!p1) return p2;
        if(!p2) return p1;
        if(p1->val <= p2->val){
            p1->next = merge(p1->next, p2);
            return p1;
        } else {
            p2->next = merge(p1, p2->next);
            return p2;
        }
    }

     ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0) return nullptr;
        ListNode* head = lists[0];
        for(int i = 1; i<lists.size(); ++i){
            if(lists[i]) head = merge(head, lists[i]);
        }
        return head;  
    }
};
```

[思路三](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/c-you-xian-dui-lie-liang-liang-he-bing-fen-zhi-he-/)：

突破点：`分治合并。`

步骤：

1. 从头开始，两两分治合并链表；
2. 最后合并剩余的两个链表。

代码：

```c++
class Solution {
public:
    // 合并两个有序链表
    ListNode* merge(ListNode* p1, ListNode* p2){
        if(!p1) return p2;
        if(!p2) return p1;
        if(p1->val <= p2->val){
            p1->next = merge(p1->next, p2);
            return p1;
        }else{
            p2->next = merge(p1, p2->next);
            return p2;
        }
    }

    ListNode* merge(vector<ListNode*>& lists, int start, int end){
        if(start == end) return lists[start];
        int mid = (start + end) / 2;
        ListNode* l1 = merge(lists, start, mid);
        ListNode* l2 = merge(lists, mid+1, end);
        return merge(l1, l2);
    }

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0) return nullptr;
        return merge(lists, 0, lists.size()-1);
    }
};
```

---

### 题目215:[数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

---

描述：

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

[思路](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/solution/215-by-ikaruga/)：

突破点：`小顶堆。`

步骤：

1. 使用优先队列建立k大小的小顶堆，堆顶即为所求；
2. 每次直接与堆顶元素进行判断，是否加入堆中。

代码：

```c++
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> pq;
        for (auto n : nums) {
            if (pq.size() == k && pq.top() >= n) continue;
            if (pq.size() == k) {
                pq.pop();
            }
            pq.push(n);
        }
        return pq.top();
    }
```

