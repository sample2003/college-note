# 1. 数组中重复的元素

## 题目

找出数组中重复的数字。

在一个长度为n的数组nums里的所有数字都在 0~n-1 的范围内。数组中某些数字是重复的,但不知道有几个数字重复了,也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例1:
输入: [2,3,1,0,2,5,3]
输出: 2或3

限制: 2 <= n <= 100000

## 思路

- 由于数组元素的值域是 0 到 n-1，可以利用数组的索引来找出重复的元素。
- 对于每个元素 nums[i]，如果 nums[nums[i]] 不等于 nums[i]，则将nums[nums[i]] 的值与 nums[i] 交换，直到找到重复的元素。

## 代码

```java
public int findRepeatNumber(int[] nums) {  
	for (int i = 0; i < nums.length; i++) {  
		while (i != nums[i]) {  
			if (nums[i] == nums[nums[i]]) {  
				return nums[i];  
			} 
			int k = nums[nums[i]];  
			nums[nums[i]] = nums[i];  
			nums[i] = k;  
		}  
	}  
	return -1;  
}
```

## 效率

- 时间复杂度是 O(n)，因为每个元素最多被访问两次。
- 空间复杂度是 O(1)，不占用额外空间。

# 2. 二维数组中查找

## 题目

在一个 n \* m 的二维数组中,每一行都按照从左到右递增的顺序排序,每一列都按照从上到下递增的顺序排序。请完成一个高效的函数,输入这样的一个二维数组和一个整数,判断数组中是否含有该整数。

示例:
现有矩阵 matrix 如下:

[
	[ 1,  4,  7, 11, 15],
	[ 2,  5,  8, 12, 19],
	[ 3,  6,  9, 16, 22],
	[10, 13, 14, 17, 24],
	[18, 21, 23, 26, 30]
\]

给定target=5,返回 true。
给定target=20,返回 false。

## 思路

- 使用从右上角或左下角开始的搜索方法。
- 由于每一行和每一列都是递增排序的，我们可以利用这个性质来快速定位到目标值或者确定目标值不存在于数组中。
- 从右上角开始，如果当前元素大于目标值，则向下移动；如果小于目标值，则向左移动。

## 代码

```java
public boolean searchMatrix(int[][] matrix, int target) {  
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;  
    int rows = matrix.length, cols = matrix[0].length;  
    int row = 0, col = cols - 1; // 从右上角开始  
    while (row < rows && col >= 0) {  
        if (matrix[row][col] == target) {  
            return true; // 找到了目标值  
        } else if (matrix[row][col] > target) {  
            col--; // 当前值大于目标值，向左移动  
        } else {  
            row++; // 当前值小于目标值，向下移动  
        }  
    }  
    return false; // 遍历完所有可能的值都没有找到目标值  
}
```

## 效率

- 时间复杂度：最坏情况下，搜索可能需要进行 `rows + cols - 1` 次比较，因此时间复杂度为 O( rows + cols )。
- 空间复杂度：O(1)，只需要常数级别的额外空间。

# 3. 替换空格

## 题目

请实现一个函数,把字符串 s 中的每个空格替换成"%20"。

示例1:
输入: s = "We are happy."
输出: "We%20are%20happy."

限制: 0 <= s 的长度 <= 10000

## 思路

通过遍历字符串 `s` 并逐个检查每个字符来解决。如果字符是空格，则用 "%20" 替换；如果不是空格，则保持不变。

## 代码

```java
public String replaceSpace(String s) {  
    StringBuilder result = new StringBuilder();  
    for (int i = 0; i < s.length(); i++) {  
        if (s.charAt(i) == ' ') {  
            result.append("%20");  
        } else {  
            result.append(s.charAt(i));  
        }  
    }  
    return result.toString();  
}
```

## 效率

- 时间复杂度：O(n)，其中 n 是字符串 `s` 的长度。我们需要遍历整个字符串来检查每个字符。
- 空间复杂度：O(n)，因为我们需要构建一个新的字符串来存储结果，其长度最多是原字符串长度的两倍（每个空格被 "%20" 替换，增加了两个字符）。

# 4. 从尾到头打印链表

## 题目

输入一个链表的头节点,从尾到头反过来返回每个节点的值(用数组返回)。

示例1:
输入: head = [1,3,2]
输出: [2,3,1]

限制: 0 <= 链表长度 <= 10000

## 思路

- 采用递归或迭代的方式来反转链表。
- 由于题目要求从尾到头返回每个节点的值，我们可以先使用迭代的方式遍历链表，将其所有节点的值存储在一个栈中，然后从栈顶到栈底弹出元素到数组中，这样就得到了从尾到头的节点值序列。

## 代码

```java
public int[] reversePrint(ListNode head) {  
    if (head == null) {  
        return new int[]{};  
    }  
    Stack<ListNode> stack = new Stack<>();  
    ListNode current = head;  
    while (current != null) {  
        stack.push(current);  
        current = current.next;  
    }  
    int[] result = new int[stack.size()];  
    while (!stack.isEmpty()) {  
        result[stack.size() - 1] = stack.pop().val;  
    }  
    return result;  
}
```

## 效率

- 时间复杂度：O(n)，其中 n 是链表的长度。我们需要遍历整个链表一次，并将所有节点压入栈中。
- 空间复杂度：O(n)，我们需要一个栈来存储所有节点，栈的大小与链表的长度相同。

# 5. 重建二叉树

## 题目

输入某二叉树的前序遍历和中序遍历的结果,请构建该二叉树并返回其根节点。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^Vto3axosQt0c3p2vZuBNN|重建二叉树图]]

示例1：
输入： preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出： [3,9,20,null,null,15,7]


示例2：
输入: preorder = [-1], inorder = [-1]
输出: [3,9,20,null,null,15,7]


## 思路

- 构建二叉树的问题可以通过递归解决。
- 前序遍历的第一个元素是树的根节点。
- 在中序遍历中找到这个根节点，就可以将左子树和右子树分开。
- 在前序遍历中，根节点后的元素分为两部分，分别对应中序遍历中根节点左边的子树和右边的子树。利用这个性质，可以递归地构建左右子树。

## 代码

```java
Map<Integer, Integer> map = new HashMap<>();  

public TreeNode buildTree(int[] preorder, int[] inorder) {  
    if (preorder == null || preorder.length == 0) {  
        return null;  
    }  
    for (int i = 0; i < inorder.length; i++) {  
        map.put(inorder[i], i);  
    }  
    return buildTreeHelper(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1);  
}  
  
private TreeNode buildTreeHelper(int[] preorder, int preStart, int preEnd, int[] inorder, int inStart, int inEnd) {  
    if (preStart > preEnd || inStart > inEnd) {  
        return null;  
    }  
  
    TreeNode root = new TreeNode(preorder[preStart]);  
    int inIndex = map.get(preorder[preStart]);  
  
    int leftTreeSize = inIndex - inStart;  
  
    root.left = buildTreeHelper(preorder, preStart + 1, preStart + leftTreeSize, inorder, inStart, inIndex - 1);  
    root.right = buildTreeHelper(preorder, preStart + leftTreeSize + 1, preEnd, inorder, inIndex + 1, inEnd);  
  
    return root;  
}
```

## 效率

# 6. 用两个栈实现队列

## 题目

用两个栈实现一个队列。队列的声明如下,请实现它的两个函数 appendTail 和deleteHead,分别完成在队列尾部插入整数和在队列头部除整数的功能。(若队列中没有元素,deleteHead 操作返回-1)

示例1：
`
输入: 
第一个栈：["CQueue","appendTail","deleteHead","deleteHead"]
第二个栈：\[[],[3],[],[]\]
输出: [null,null,3,-1]

示例2：

输入:
第一个栈： ["CQueue","deleteHead","appendTail","appendTail","deleteHead"]
第二个栈：\[[],[],[5],\[2],[],[]\]
输出: [null,-1,null,null,5,2]

提示:
>. 1 <= values <= 10000
>· 最多会对 appendTail、deleteHead 进行 10000 次调用

## 思路

- 使用两个栈 `stack1` 和 `stack2`，其中 `stack1` 用于插入元素，`stack2` 用于删除元素。
- 当调用 `appendTail` 时，直接将元素压入 `stack1`。
- 当调用 `deleteHead` 时，如果 `stack2` 不为空，直接弹出栈顶元素；如果 `stack2`为空，将 `stack1` 中的元素依次弹出并压入 `stack2`，然后再弹出栈顶元素。

## 代码

```java
class CQueue {  
    private Stack<Integer> stack1;  // 第一个栈，用于插入元素  
    private Stack<Integer> stack2;  // 第二个栈，用于删除元素  
  
    public CQueue() {  
        stack1 = new Stack<>();  
        stack2 = new Stack<>();  
    }  
  
    // 在队列尾部插入整数  
    public void appendTail(int value) {  
        stack1.push(value);  
    }  
  
    // 在队列头部删除整数  
    public int deleteHead() {  
        if (stack2.isEmpty()) {  
            // 如果第二个栈为空，将第一个栈中的元素依次弹出并压入第二个栈  
            while (!stack1.isEmpty()) {  
                stack2.push(stack1.pop());  
            }  
        }  
        if (stack2.isEmpty()) {  
            // 如果第二个栈依然为空，说明队列中没有元素，返回-1  
            return -1;  
        } else {  
            // 弹出第二个栈的栈顶元素  
            return stack2.pop();  
        }  
    }  
}
```

## 效率

# 7. 斐波那契数列

## 题目

写一个函数,输入`n`,求斐波那契(Fibonacci)数列的第`n`项(即F(N))。嬰波那契数列的定义如下:
```
F(0) = 0, F(1) = 1
F(N)=F(N-1)+F(N-2),其中N>1.
```

斐波那契数列由0和1开始,之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模1e9+7(1000000007),如计算初始结果为:1000000008,请返回1。

示例1：
输入: n=2
输出: 1

示例2：
输入: n=5
输出: 5

## 思路

1. 动态规划
	- 使用动态规划的思想，从前往后计算斐波那契数列的值。
	- 初始时，设定 `a = 0`，`b = 1`，然后根据斐波那契数列的定义，依次计算出第 `2` 到第 `n` 项的值。
	- 由于题目要求对结果取模 `1e9+7`，因此在每次计算后都要取模。
2. 递归
	- 当 `n` 小于等于 1 时，直接返回 `n`。
	- 否则，斐波那契数列的第 `n` 项等于第 `n-1` 项加上第 `n-2` 项的和。


## 代码

```java
// 动态规划
public int fib(int n) {
	if (n == 0) {
		return 0;
	}
	if (n == 1) {
		return 1;
	}
	
	int a = 0;
	int b = 1;
	int sum;
	
	for (int i = 2; i <= n; i++) {
		sum = (a + b) % 1000000007;
		a = b;
		b = sum;
	}
	
	return b;
}

// 递归
public int fibonacci(int n) { 
	if (n <= 1) { return n; } 
	return fibonacci(n - 1) + fibonacci(n - 2); 
}
```

## 效率

1. 动态规划
	- 时间复杂度：O(n)，需要计算出第 `n` 项的斐波那契数列值。
	- 空间复杂度：O(1)，只需要常数级别的额外空间。
2. 递归
   - 时间复杂度：递归的时间复杂度也较高，为指数级别，大约为 O(2^n)。
   - 空间复杂度：O(n)。

# 8. 青蛙跳台阶问题

## 题目

一只青蛙一次可以跳上1级台阶,一可以跳上2级台阶。求该青蛙跳上一个`n`级的台阶总共有多少种跳法。

答案需要取模1e9+7(1000000007),如计算初始结果为 1000000008,请返回1。

示例1:
输入: n = 2
输出: 2

示例2:
输入: n = 7
输出: 21

示例3:
输入: n = 0
输出: 1

提示: 0 <= n <= 100

## 思路

1. 动态规划
	- 使用动态规划的思想，从前往后计算青蛙跳台阶的方法总数。
	- 初始时，设定`a = 1`，`b = 1`，表示跳上 `0` 级和跳上 `1` 级台阶的方法总数。
	- 然后根据青蛙跳台阶的规律，依次计算出跳上 `2` 到 `n` 级台阶的方法总数。
	- 每次计算后都要取模 `1e9+7`。
2. 递归
	- 当 `n` 为 0 或 1 时，直接返回 1。
	- 否则，青蛙跳上 `n` 级台阶的方法总数等于跳上 `n-1` 级台阶的方法总数加上跳上 `n-2` 级台阶的方法总数的和。

## 代码

```java
// 动态规划
public int numWays(int n) {
	// 如果台阶数为 0 或 1，直接返回 1
	if (n == 0 || n == 1) {
		return 1;
	}
	
	// 初始化 a 和 b，表示跳上 0 级和跳上 1 级台阶的方法总数
	int a = 1;
	int b = 1;
	int sum;
	
	// 从 2 开始循环计算跳上 2 到 n 级台阶的方法总数
	for (int i = 2; i <= n; i++) {
		sum = (a + b) % 1000000007;  // 计算当前台阶数的方法总数，并取模
		a = b;  // 更新 a 的值为上一次的 b
		b = sum;  // 更新 b 的值为当前计算出的方法总数
	}
	
	return b;  // 返回跳上 n 级台阶的方法总数
}

// 递归
public int numWays(int n) { 
	if (n == 0 || n == 1) { return 1; } 
	return (numWays(n - 1) + numWays(n - 2)) % 1000000007; 
}
```

## 效率

1. 动态规划
	- 时间复杂度：O(n)，需要计算跳上 `n` 级台阶的方法总数。
	- 空间复杂度：O(1)，只需要常数级别的额外空间。

2. 递归
	- 时间复杂度：递归的时间复杂度较高，为指数级别，大约为 O(2^n)。
	- 空间复杂度：递归的空间复杂度也较高，为 O(n)。

# 9. 旋转数组的最小值

## 题目
把一个数组最开始的若干个元素搬到数组的末尾,我们称之为数组的旋转。

给你一个可能存在 `重复` 元素值的数组 numbers,它原来是一个`升序排列的数组`,并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如,数组[3,4,5,1,2]为[1,2,3,4,5]的一次旋转,该数组的最小值为1。

注意,数组[a[0],a[1],a[2],…a[n-1]] 旋转一次的结果为
数组[a[n-1],a[0],a[1],a[2],...,a[n-2]]

示例1:
输入: numbers = [3,4,5,1,2]
输出: 1

示例2:
输入: numbers = [2,2,2,0,1]
输出: 0

提示:
-  n == numbers.length
- 1 <= n <= 5000
- -5000 <= numbers[i] <= 5000
- numbers 原来是一个升序排序的数组,并进行了1至 n 次旋转

## 思路

- 使用二分查找的方式来寻找旋转数组的最小元素。
- 初始化左右指针，然后在每一步中，找到中间值，并根据中间值与右边界值的大小关系来更新左右指针的位置。
- 如果中间值小于右边界值，则说明最小值位于中间值的左侧，将右指针移动到中间值处。
- 如果中间值大于右边界值，则说明最小值位于中间值的右侧，将左指针移动到中间值的下一个位置。
- 如果中间值等于右边界值，则将右指针向左移动一位。

## 代码

```java
public int findMin(int[] numbers) {  
    int left = 0, right = numbers.length - 1;  
  
    while (left < right) {  
        int mid = left + (right - left) / 2;  
  
        if (numbers[mid] < numbers[right]) {  
            right = mid;  
        } else if (numbers[mid] > numbers[right]) {  
            left = mid + 1;  
        } else { // 处理重复元素  
            right--;  
        }  
    }  
    return numbers[left];  
}
```

## 效率

- 时间复杂度：二分查找的时间复杂度为 O(log n)。
- 空间复杂度：该算法使用常数级别的额外空间，空间复杂度为 O(1)。

# 10. 矩阵中的路径

## 题目

给定一个 m x n 二维字符网格 board 和一个字符串单词 word。如果 word 存在于网格中,返回 true;否则,返回 false。单词必须按照字母顺序,通过相邻的单元格内的字母构成,其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

例如,在下面的3×4的矩阵中包含单词“ABCCED”(单词中的字母已标出)。

[
	[ A, B, C, E],
	[ S, F, C, S],
	[ A, D, E, E]
]

## 思路

- 遍历二维字符网格中的每个位置，以每个位置为起点进行深度优先搜索（DFS）。
- 在DFS中，递归地判断当前位置是否匹配单词中的字符，若匹配则继续向上下左右四个方向搜索。
- 使用一个额外的二维数组来标记已访问过的位置，避免重复访问。

## 代码

```java
public boolean exist(char[][] board, String word) {  
    int m = board.length;  
    int n = board[0].length;  
  
    for (int i = 0; i < m; i++) {  
        for (int j = 0; j < n; j++) {  
            if (dfs(board, i, j, word, 0)) {  
                return true;  
            }  
        }  
    }  
  
    return false;  
}  
  
private boolean dfs(char[][] board, int i, int j, String word, int index) {  
    if (index == word.length()) {  
        return true;  
    }  
  
    if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(index)) {  
        return false;  
    }  
  
    char temp = board[i][j];  
    board[i][j] = ' '; // 标记已访问过的位置  
  
    boolean found = dfs(board, i + 1, j, word, index + 1) ||  
            dfs(board, i - 1, j, word, index + 1) ||  
            dfs(board, i, j + 1, word, index + 1) ||  
            dfs(board, i, j - 1, word, index + 1);  
  
    board[i][j] = temp; // 恢复原字符  
  
    return found;  
}
```

## 效率

- 时间复杂度：遍历二维网格的时间复杂度为 O(m\*n)，每个位置进行DFS的时间复杂度为 O(4^k)，其中 k 是单词的长度。
- 空间复杂度：递归调用的栈空间复杂度为 O(k)，额外的标记数组空间复杂度为 O(m\*n)。

# 11. 机器人的运动范围

## 题目

地上有一个m行n列的方格,从坐标[0,0]到坐标[m-1,n-1]。一个机器人从坐标[0,0]的格子开始移动,它每次可以向左、右、上、下移动一格(不能移动到方格外),也不能进入行坐标和列坐标的数位之和大于 `k` 的格子。例如,当k为18时,机器人能够进入方格[35,37],因为3+5+3+7=18。但它不能进入方格[35,38],因为3+5+3+8=19。请问该机器人能够到达多少个格子?

示例1:
输入: m = 2, n = 3, k = 1
输出: 3

示例2:
输入: m = 3, n = 1, k = 0
输出: 1

提示:
- 1 <= n,m <= 100
- 0 <= k <= 20

## 思路

- 代码使用深度优先搜索（DFS）的方式遍历方格中的每个位置，判断是否满足条件，并统计满足条件的格子数量。
- 从起点开始，递归地向上下左右四个方向搜索，并在搜索过程中进行边界判断、访问标记和数位之和判断。

## 代码

```java
// 这个方法接受三个参数：方格的行数 m、列数 n，以及限制条件 k。它返回一个整数，表示机器人能够到达的格子数量。  
public int movingCount(int m, int n, int k) {  
    // 首先创建一个大小为 m×n 的二维布尔数组 visited，用于标记方格中的位置是否已经被访问过。  
    boolean[][] visited = new boolean[m][n];  
    // 然后调用 dfs 方法从坐标 [0, 0] 开始进行深度优先搜索，统计满足条件的格子数量。  
    return dfs(0, 0, m, n, k, visited);  
}  
  
// 这是一个辅助方法，用于进行深度优先搜索。  
//参数包括当前位置的行索引 i、列索引 j，方格的行数 m、列数 n，限制条件 k，以及用于标记已访问位置的二维布尔数组 visited。  
private int dfs(int i, int j, int m, int n, int k, boolean[][] visited) {  
    // 首先进行边界判断，如果当前位置越界、已经访问过或数位之和大于 k，则返回 0。  
    if (i < 0 || i >= m || j < 0 || j >= n || visited[i][j] || getDigitSum(i) + getDigitSum(j) > k) {  
        return 0;  
    }  
  
    //标记当前位置为已访问。  
    visited[i][j] = true;  
  
    //然后递归地向上下左右四个方向搜索，并将每个方向的结果累加起来。  
    return 1 + dfs(i + 1, j, m, n, k, visited) + dfs(i - 1, j, m, n, k, visited) +  
            dfs(i, j + 1, m, n, k, visited) + dfs(i, j - 1, m, n, k, visited);  
    //在递归调用结束后，返回当前位置能够到达的格子数量。  
}  
  
//这是一个辅助方法，用于计算一个数的数位之和。  
private int getDigitSum(int num) {  
    int sum = 0;  
    //参数为一个整数 num，返回数位之和的结果。  
    while (num > 0) {  
        sum += num % 10;  
        num /= 10;  
    }  
    return sum;  
}
```

## 效率

- 时间复杂度：遍历所有的格子，时间复杂度为 O(m\*n)。
- 空间复杂度：递归调用的栈空间复杂度为 O(mn)，额外的标记数组空间复杂度为 O(mn)。

# 12. 剪绳子 Ⅰ

## 题目

给你一根长度为`n`的绳子,请把绳子剪成整数长度的`m`段(m、n都是整数,n>1并且m>1),每段绳子的长度记为k[0],k[1].k[m-1]。请问k[0]\*k[1] \*...\* k[m-1] 可能的最大乘积是多少？例如,当绳子的长度是8时,我们把它剪成长度分别为2、3、3的三段,此时得到的最大乘积是18。

示例1:
输入: 2
输出: 1
解释: 2 = 1+1, 1×1 = 1

示例2:
输入: 10
输出: 36
解释: 10 = 3+3+4, 3×3×4 = 36

提示: 2 <= n <= 58

## 思路

- 当 n <= 3 时，由于题目要求 m > 1，因此返回 n - 1。
- 当 n > 3 时，尽可能多地剪长度为 3 的段，并且尽量不要剩下长度为 1 的段，因为 3_1 < 2_2。
- 因此，计算 n 除以 3 的商 a 和余数 b，然后根据 b 的不同情况返回不同的乘积结果。

## 代码

```java
// 这个方法接受一个整数 n 作为输入，表示绳子的长度。  
public int cuttingRope(int n) {  
    // 首先进行特殊情况的处理，当 n 小于等于 3 时，返回 n - 1。  
    if (n <= 3) {  
        return n - 1;  
    }  
    // 对于 n 大于 3 的情况，计算 n 除以 3 的商 a 和余数 b。  
    int a = n / 3;  
    int b = n % 3;  
  
    //根据余数 b 的不同情况，返回不同的乘积结果：  
    if (b == 0) {  
        //如果余数 b 等于 0，则返回 3 的 a 次方。  
        return (int) Math.pow(3, a);  
    } else if (b == 1) {  
        //如果余数 b 等于 1，则返回 3 的 (a-1) 次方 乘以 4。  
        return (int) (Math.pow(3, a - 1) * 4);  
    } else {  
        //如果余数 b 等于 2，则返回 3 的 a 次方 乘以 2。  
        return (int) (Math.pow(3, a) * 2);  
    }  
}
```

## 效率

- 时间复杂度：O(1)，算法的时间复杂度与输入 n 无关。
- 空间复杂度：O(1)，算法的空间复杂度是常数级别的。

# 13. 剪绳子 Ⅱ

## 题目

给你一根长度为 n 的绳子,请把绳子剪成整数长度的 m段(m、n都是整数,n>1并且m>1),每段绳子的长度记为 k[0],k[1] ... k[m-1]。请问k[0]\*k[1] \*...\* k[m-1] 可能的最大乘积是多少?例如,当绳子的长度是8时,我们把它剪成长度分别为2、3、3的三段,此时得到的最大乘积是18。
答案需要取模1e9+7(1000000007),如计算初始结果为:1000000008,请返回1。

示例1:

示例1:
输入: 2
输出: 1
解释: 2 = 1+1, 1×1 = 1

示例2:
输入: 10
输出: 36
解释: 10 = 3+3+4, 3×3×4 = 36

提示: 2 <= n <= 1000

## 思路

- 当 n <= 3 时，由于题目要求 m > 1，因此返回 n - 1。
- 当 n > 3 时，尽可能多地剪长度为 3 的段，并且尽量不要剩下长度为 1 的段，因为 3\*1 < 2\*2。
- 在计算的过程中，使用 long 类型来存储中间结果，并在每一步计算后取模 1000000007，以防止结果溢出。
## 代码

```java
// 这个方法接受一个整数 n 作为输入，表示绳子的长度。  
public int cuttingRope(int n) {  
    // 首先进行特殊情况的处理，当 n 小于等于 3 时，返回 n - 1。  
    if (n <= 3) {  
        return n - 1;  
    }  
  
    long res = 1;  
    // 对于 n 大于 3 的情况，使用循环尽可能多地剪长度为 3 的段，  
    // 并且在每一步计算后取模 1000000007，以防止结果溢出。  
    while (n > 4) {  
        res = (res * 3) % 1000000007;  
        n -= 3;  
    }
    // 最后返回结果
    return (int) (res * n % 1000000007);  
}
```

## 效率

- 时间复杂度：O(log n)，算法的时间复杂度与输入 n 的大小有关。
- 空间复杂度：O(1)，算法的空间复杂度是常数级别的。

# 14. 二进制中1的个数

## 题目

编写一个函数, 输入是一个无符号整数(以二进制串的形式), 返回其二进制表达式中数字位数为'1'的个数(也被称为汉明重量))。

提示:
- 请注意,在某些语言(如Java)中,没有无符号整数类型。在这种情况下,输入和输出都将被指定为有符号整数类型,并且不应影响您的实现,因为无论整数是有符号的还是无符号的,其内部的二进制表示形式都是相同的。
- 在Java中,编译器使用 二进制补码 记法来表示有符号整数。因此,在上面的示例3中,输入表示有符号整数 -3。

示例1:
输入: n = 11(控制台输入00000000000000000000000000001011)
输出: 3
解释: 输入的二进制串 00000000000000000000000000001011 中,共有三位为'1'。

## 思路

- 这里使用了一个经典的位运算技巧，即 n & (n-1) 可以消除 n 的二进制表示中最右边的 1。
- 我们循环执行 n & (n-1)，每执行一次，就将 n 的二进制表示中的一个 1 变为 0，直到 n 变为 0 为止，统计执行的次数即为 1 的个数。

## 代码

```java
public int hammingWeight(int n) {  
    int count = 0;  
    while (n != 0) {  
        count++;  
        n = n & (n - 1);  
    }  
    return count;  
}
```

## 效率

- 时间复杂度：O(k)，其中 k 是 n 的二进制表示中 1 的个数。
- 空间复杂度：O(1)，算法的空间复杂度是常数级别的。

# 15. 数值的整数次方

## 题目

实现pow(x,n),即计算x的n次幂函数(即,xn)。不得使用库函数,同时不需要考虑大数问题。

示例1:
输入: x=2.00000, n = 10
输出: 1024.00000

示例2:
输入: x = 2.10000, n = 3
输出: 9.26100

示例3:
输入: x = 2.00000, n = -2
输出: 0.25000
解释: 2^-2 = 1/2^2 = 1/4 = 0.25

提示：
- -100.0 < x < 100.0
- -2^31 <= n <= 2^31-1
- -10^4 <= x^n <= 10^4

## 思路

- 针对指数 n 的正负分别处理，如果 n < 0，则将 x 变为 1/x，n 变为 -n。
- 使用循环的方式，每次将 x 自乘，n 变为 n/2，直到 n 变为 0。
- 如果 n 的当前位为 1，则将结果乘以当前 x。

## 代码

```java
// 这个方法接受一个双精度浮点数 x 和一个整数 n 作为输入，表示要计算 x 的 n 次幂。  
public double myPow(double x, int n) {  
    // 首先判断 n 是否为 0，如果是，则直接返回 1。  
    if (n == 0) {  
        return 1;  
    }  
    // 如果 n 小于 0，则将 x 变为 1/x，n 变为 -n，这样处理是为了处理负指数的情况。  
    if (n < 0) {  
        x = 1 / x;  
        n = -n;  
    }  
    double result = 1;  
    // 然后使用循环的方式，每次将 x 自乘，n 变为 n/2，直到 n 变为 0。  
    while (n > 0) {  
        // 如果 n 的当前位为 1，则将结果乘以当前 x。  
        if (n % 2 == 1) {  
            result *= x;  
        }  
        x *= x;  
        n /= 2;  
    }  
    // 最后返回计算得到的结果。  
    return result;  
}
```

## 效率

- 时间复杂度：O(log n)，其中 n 是指数的绝对值。
- 空间复杂度：O(1)，算法的空间复杂度是常数级别的。

# 16. 打印从1到最大的n位数

## 题目

输入数字 n,按顺序打印出从1到最大的n位十进制数。比如输入3,则打印出1、2、3一直到最大的3位数999A

示例1:
输入:n=1
输出:[1,2,3,4,5,6,7,8,9]

说明:
- 用返回一个整数列表来代替打印
- n 为正整数

## 思路

- 首先计算最大的 n 位十进制数，即 10 的 n 次方减去 1。
- 然后创建一个长度为最大数的整数数组，依次填入从 1 到最大数的值。
- 返回填充好的整数数组。

## 代码

```java
//这个方法接受一个整数 n 作为输入，表示要打印的最大 n 位十进制数。  
public int[] printNumbers(int n) {  
    //首先计算最大的 n 位十进制数，即 10 的 n 次方减去 1，这里使用了 Math.pow 函数来计算。  
    int max = (int) Math.pow(10, n) - 1;  
    //然后创建一个长度为最大数的整数数组 result。  
    int[] result = new int[max];  
    //使用循环将从 1 到最大数的值依次填入 result 数组中。  
    for (int i = 0; i < max; i++) {  
        result[i] = i + 1;  
    }  
    //最后返回填充好的整数数组。  
    return result;  
}
```

## 效率

- 时间复杂度：O(10^n)，需要填充从 1 到最大 n 位数的整数数组。
- 空间复杂度：O(1)，除了返回的整数数组外，算法的空间复杂度是常数级别的。

# 17. 删除链表的节点

## 题目

给定单向链表的头指针和一个要删除的节点的值,定义一个函数删除该节点。返回删除后的链表的头节点。
注意:此题对比原题有改动

示例1:
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点, 那么在调用了你的函数之后, 该链表应变为 4->1->9.

示例2:
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点, 那么在调用了你的函数之后, 该链表应变为 4->5->9.

说明: 题目保证链表中节点的值互不相同

## 思路

- 遍历链表，找到要删除的节点的前一个节点 prev 和要删除的节点 curr。
- 将 prev 的 next 指向 curr 的下一个节点，实现删除操作。

## 代码

```java
// 这个方法接受链表的头节点 head 和要删除的节点值 val 作为输入。  
public ListNode deleteNode(ListNode head, int val) {  
    if (head == null) {  
        return null;  
    }  
    //首先处理特殊情况，如果头节点的值就是要删除的值 val，则直接返回头节点的下一个节点，即删除头节点。  
    if (head.val == val) {  
        return head.next;  
    }  
    ListNode prev = head;  
    ListNode curr = head.next;  
    //遍历链表找到要删除的节点的前一个节点 prev 和要删除的节点 curr。  
    while (curr != null && curr.val != val) {  
        //将 prev 的 next 指向 curr 的下一个节点，实现删除操作。  
        prev = curr;  
        curr = curr.next;  
    }  
    if (curr != null) {  
        prev.next = curr.next;  
    }  
    //最后返回头节点 head。  
    return head;  
}
```

## 效率

- 时间复杂度：O(N)，其中 N 是链表的长度。最坏情况下，需要遍历整个链表找到要删除的节点。
- 空间复杂度：O(1)，只使用了常数级别的额外空间。


# 18. 正则表达式匹配

## 题目

请实现一个函数用来匹配包含'.', 和 '\*' 的正则表达式。模式中的字符'.'表示任意一个字符, 而'\*'表示它前面的字符可以出现任意次(含0次)。在本题中,匹配是指字符串的所有字符匹配整个模式。例如,字符串"aaa"与模式"a.a"和"ab\*ac\*a"匹配,但与"aa.a"和"ab\*a"均不匹配。

示例1:
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。

示例2:
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为'\*'代表可以匹配零个或多个前面的那一个元素,在这里前面的元素就是'a'。因此,字符串"aa"可被视为'a'重复了一次。

示例3：
输入:
s = "ab"
p = ".\*"
输出: true
解释: ".\*"表示可匹配零个或多个('\*')任意字符('.')。

示例 4:
输入:
S = "aab"
p = "c\*a\*b"
输出: true
解释: 因为'\*'表示零个或多个, 这里'c'为0个,'a'被重复一次。因此可以匹配字符串"aab"。

示例5:
输入:
s = "mississippi"
p = "mis\*is\*p\*."
输出: false

提示：
- s可能为空, 且只包含从 a-z 的小写字母。
- p可能为空, 且只包含从 a-z 的小写字母和字符'.'和'\*'。

## 思路

- 使用递归的方式进行匹配。
- 首先判断模式 p 是否为空，如果为空，则判断字符串 s 是否为空，如果也为空则返回 true，否则返回 false。
- 然后判断第一个字符是否匹配，如果匹配则继续匹配剩余部分，如果不匹配则返回 false。
- 如果模式 p 的第二个字符是 '\*'，则有两种情况：
  1. * 匹配 0 次，直接跳过 * 和它前面的字符；
  2. * 匹配 1 次或多次，继续匹配字符串 s 的下一个字符和模式 p。

## 代码

```java
public boolean isMatch(String s, String p) {  
    // 首先检查模式字符串 p 是否为空，如果为空，就判断字符串 s 是否也为空，  
    // 如果是则返回 true，表示匹配成功；否则返回 false，表示匹配失败。  
    if (p.isEmpty()) {  
        return s.isEmpty();  
    }  
    // 接着判断字符串 s 的第一个字符和模式字符串 p 的第一个字符是否匹配。  
    // 如果匹配，就继续匹配剩余部分；如果不匹配，就返回 false。  
    boolean firstMatch = (!s.isEmpty() && (p.charAt(0) == s.charAt(0) || p.charAt(0) == '.'));  
    // 如果模式字符串 p 的第二个字符是 '*'，则有两种情况需要考虑：  
    if (p.length() >= 2 && p.charAt(1) == '*') {  
        // '*' 匹配 0 次：直接跳过 '*' 和它前面的字符，继续匹配剩余部分。  
        return (isMatch(s, p.substring(2)) || (firstMatch && isMatch(s.substring(1), p)));  
    } else {  
        // '*' 匹配 1 次或多次：继续匹配字符串 s 的下一个字符和模式 p。  
        return firstMatch && isMatch(s.substring(1), p.substring(1));  
    }  
}
```

## 效率

- 时间复杂度：在最坏情况下，时间复杂度为 O((T+P)2^(T+P/2))，其中 T 和 P 分别是字符串 s 和模式 p 的长度。这是因为在最坏情况下，每个字符串都有 2^(T+P/2) 种匹配方式。
- 空间复杂度：O(T^2 + P^2)，其中 T 和 P 分别是字符串 s 和模式 p 的长度。递归调用的最大深度为 T+P。

# 19. 表示数值的字符串

## 题目

请实现一个函数用来判断字符串是否表示数值(包括整数和小数)。

数值(按顺序)可以分成以下几个部分:
1. 若干空格
2. 一个 小数 或者 整数
3. (可选)一个'e'或'E',后面跟着一个整数
4. 若干空格

小数(按顺序)可以分成以下几个部分:
1. (可选)一个符号字符('+'或'-')
2. 下述格式之一:
	1. 至少一位数字,后面跟着一个点'.'
	2. 至少一位数字,后面跟着一个点'.', 后面跟着至少一位数字
	3. 一个点'.', 后面跟着至少一位数字

整数(按顺序)可以分成以下几个部分:
1. (可选)一个符号字符('+'或'-')
2. 至少一位数字

部分数值列举如下:
["+100","5e2","-123","3.1416","-1E-16","0123"]

部分非数值列举如下:
["", " ", "abc", "1a", "1+1", "1.", ".1", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"]

## 思路

1. 首先去除字符串两端的空格。
2. 使用四个标志位来跟踪是否已经遇到过数字、指数、小数点和符号。
3. 遍历字符串中的每个字符:
    - 如果是数字字符, 则设置 `seenDigit` 标志位为 true。
    - 如果是 'e' 或 'E', 则需要检查是否已经遇到过指数和数字, 如果没有遇到过数字或已经遇到过指数, 则返回 false。同时更新 `seenExponent` 标志位为 true, 并将 `seenDigit` 标志位设为 false。
    - 如果是 '+' 或 '-', 则需要检查它们是否出现在指数部分或者是否已经出现过, 如果是, 则返回 false。同时更新 `seenSign` 标志位为 true。
    - 如果是 '.', 则需要检查是否已经遇到过小数点和指数, 如果是, 则返回 false。同时更新 `seenDot` 标志位为 true。
    - 如果是其他字符, 则返回 false。
4. 最后检查是否已经遇到过数字, 如果是, 则返回 true, 否则返回 false。

## 代码

```java
public boolean isNumber(String s) {  
    // 去除前后空格  
    s = s.trim();  
  
    // 用于标记是否已经遇到过数字  
    boolean seenDigit = false;  
    // 用于标记是否已经遇到过指数部分  
    boolean seenExponent = false;  
    // 用于标记是否已经遇到过小数点  
    boolean seenDot = false;  
    // 用于标记是否已经遇到过正负号  
    boolean seenSign = false;  
  
    for (int i = 0; i < s.length(); i++) {  
        char c = s.charAt(i);  
        // 如果是数字字符(c >= '0' && c <= '9'), 则设置 seenDigit 为 true。  
        if (c >= '0' && c <= '9') {  
            seenDigit = true;  
        } else if (c == 'e' || c == 'E') {  
            //如果是 'e' 或 'E':            //检查是否已经遇到过数字和指数,如果没有遇到过数字或已经遇到过指数,则返回 false。  
            if (!seenDigit || seenExponent) {  
                return false;  
            }  
            //更新 seenExponent 为 true,并将 seenDigit 设为 false。  
            seenExponent = true;  
            seenDigit = false;  
        } else if (c == '+' || c == '-') {  
                //如果是 '+' 或 '-':            if (i > 0 && s.charAt(i - 1) != 'e' && s.charAt(i - 1) != 'E' && !seenSign) {  
                //检查它们是否出现在指数部分或者是否已经出现过,如果是,则返回 false。  
                //更新 seenSign 为 true。  
                seenSign = true;  
            } else {  
                return false;  
            }  
        } else if (c == '.') {  
            //如果是 '.':            if (seenDot || seenExponent) {  
                //检查是否已经遇到过小数点和指数,如果是,则返回 false。  
                return false;  
            }  
            //更新 seenDot 为 true。  
            seenDot = true;  
        } else {  
            //如果是其他字符,则返回 false。  
            return false;  
        }  
    }  
    return seenDigit;  
}
```

## 效率

- 时间复杂度: O(n), 其中 n 是输入字符串的长度。我们只需要遍历一遍字符串。
- 空间复杂度: O(1), 我们只使用了几个常量大小的变量。

# 20. 调整数组顺序使奇数位于偶数前面

## 题目

输入一个整数数组, 实现一个函数来调整该数组中数字的顺序, 使得所有奇数在数组的前半部分, 所有偶数在数组的后半部分。

示例:
输入: nums=[1,2,3,4]
输出: [1,3,2,4]
注: [3,1,2,4]也是正确的答案之一。

提示:
- 0 <= nums.length <= 50000
- 0 <= nums[i] <= 10000


## 思路

1. 使用两个指针 `left` 和 `right` 分别指向数组的左右端。
2. 循环执行以下操作:
    - 如果当前 `left` 指针指向的元素是奇数,则将其移动到前半部分,即 `left++`。
    - 如果当前 `right` 指针指向的元素是偶数,则将其移动到后半部分,即 `right--`。
    - 如果 `left` 小于 `right`,则交换 `left` 和 `right` 指针指向的元素。
3. 循环结束后,所有奇数都在前半部分,所有偶数都在后半部分。
4. 使用 (nums[left] & 1) == 1 来判断当前元素是否为奇数,这是一种高效的方法,避免了使用 % 运算符。  
5. 在移动指针时,我们使用 left < right 作为循环条件,确保指针不会越界。

## 代码

```java
public int[] exchange(int[] nums) {  
    // 定义左右指针  
    int left = 0, right = nums.length - 1;  
    while (left < right) {  
        // 如果当前元素是奇数,则将其移动到前半部分  
        while (left < right && (nums[left] & 1) == 1) {  
            left++;  
        }  
        // 如果当前元素是偶数,则将其移动到后半部分  
        while (left < right && (nums[right] & 1) == 0) {  
            right--;  
        }  
        // 交换左右指针指向的元素  
        int temp = nums[left];  
        nums[left] = nums[right];  
        nums[right] = temp;  
    }  
    return nums;  
}
```

## 效率

- 时间复杂度: O(n), 其中 n 是数组的长度。我们只需要遍历数组一次。
- 空间复杂度: O(1), 我们只使用了两个指针和一个临时变量,空间复杂度是常数级别的。

# 21. 链表中倒数第k个节点

## 题目

输入一个链表,输出该链表中倒数第k个节点。为了符合大多数人的习惯,本题从1开始计数,即链表的尾节点是倒数第1个节点。
例如,一个链表有6 个节点,从头节点开始,它们的值依次是1、2、3、4、5、6。这个链表的倒数第3 个节点是值为 4 的节点。

示例:
给定一个链表: 1->2->3->4->5, 和 k=2.
返回链表: 4->5.

## 思路

1. 首先判断链表是否为空或 k 是否小于等于 0,如果是,直接返回 null。
2. 使用两个指针 `fast` 和 `slow`,`fast` 先走 k 步。
3. 如果 `fast` 指针提前到达链表尾部,说明 k 大于链表长度,返回 null。
4. 然后 `fast` 和 `slow` 一起移动,直到 `fast` 到达链表尾部。
5. 此时 `slow` 指针指向的就是倒数第 k 个节点,返回它。

**代码解释: **
- 在第 2 步中,我们使用 `for` 循环让 `fast` 指针先走 k 步。如果 `fast` 指针提前到达 `null`,说明 k 大于链表长度,我们直接返回 `null`。
- 在第 4 步中,我们让 `fast` 和 `slow` 指针一起移动,直到 `fast` 到达链表尾部。此时 `slow` 指针指向的就是倒数第 k 个节点。

## 代码

```java
public ListNode getKthFromEnd(ListNode head, int k) {  
    // 如果链表为空或 k 小于等于 0,返回 null    if (head == null || k <= 0) {  
        return null;  
    }  
    // 使用两个指针 fast 和 slow,fast 先走 k 步  
    ListNode fast = head;  
    for (int i = 0; i < k; i++) {  
        if (fast == null) {  
            // 如果 fast 指针提前到达链表尾部,说明 k 大于链表长度,返回 null            return null;  
        }  
        fast = fast.next;  
    }  
    // 然后 fast 和 slow 一起移动,直到 fast 到达链表尾部  
    ListNode slow = head;  
    while (fast != null) {  
        fast = fast.next;  
        slow = slow.next;  
    }  
    // 此时 slow 指针指向的就是倒数第 k 个节点  
    return slow;  
}
```

## 效率

- 时间复杂度: O(n), 其中 n 是链表的长度。我们只需要遍历链表一次。
- 空间复杂度: O(1), 我们只使用了两个指针,空间复杂度是常数级别的。

# 22. 反转链表

## 题目

定义一个函数,输入一个链表的头节点,反转该链表并输出反转后链表的头节点。

示例:
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL

限制: 0 <= 节点个数 <= 5000

## 思路

1. 如果链表为空或只有一个节点,直接返回原链表头节点。
2. 使用两个指针 `prev` 和 `current`,分别表示前一个节点和当前节点。
3. 遍历链表,在遍历过程中反转节点指针的方向。
4. 最后返回反转后的头节点。

**代码解释**:
- 在循环中,我们先保存当前节点的下一个节点 `nextNode`,然后将当前节点的指针指向前一个节点 `prev`,接着更新 `prev` 为当前节点, `current` 为下一个节点 `nextNode`。
- 循环结束后,`prev` 指向的就是原链表的最后一个节点,即反转后的头节点。
- 
## 代码

```java
public ListNode reverseList(ListNode head) {  
    // 如果链表为空或只有一个节点,直接返回原链表头节点  
    if (head == null || head.next == null) {  
        return head;  
    }  
  
    ListNode prev = null; // 前一个节点  
    ListNode current = head; // 当前节点  
  
    while (current != null) {  
        ListNode nextNode = current.next; // 保存当前节点的下一个节点  
        current.next = prev; // 反转当前节点的指针指向前一个节点  
        prev = current; // 更新前一个节点为当前节点  
        current = nextNode; // 更新当前节点为下一个节点  
    }  
  
    // 循环结束后,prev指向原链表的最后一个节点,即反转后的头节点  
    return prev;  
}
```
## 效率

- 时间复杂度: O(n), 其中 n 是链表的长度。我们需要遍历整个链表一次。
- 空间复杂度: O(1), 我们只使用了常数级别的额外空间。

# 23. 合并两个排序的链表

## 题目

输入两个递增排序的链表,合并这两个链表并使新链表中的节点仍然是递增排序的。

示例:
输入: 1->2->4, 1->3->4
输出: 1->1->2->3->4->4

限制: 0 <= 链表长度 <= 1000

## 思路

1. 创建一个虚拟头节点 `dummy`,简化操作。
2. 使用一个指针 `current` 表示当前节点,初始化为 `dummy`。
3. 循环比较 `l1` 和 `l2` 的节点,将较小的节点接在 `current` 节点的后面。
4. 将剩余的节点接在 `current` 节点后面。
5. 返回虚拟头节点的下一个节点,即合并后的链表头节点。

**代码解释**:
1. 在循环中,我们比较 `l1` 和 `l2` 的节点,将较小的节点接在 `current` 节点的后面,然后更新 `current` 和被选中节点的指针。
2. 循环结束后,可能 `l1` 或 `l2` 中还有剩余的节点,我们将剩余的节点接在 `current` 节点后面。
3. 最后返回虚拟头节点的下一个节点,即合并后的链表头节点。

## 代码

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {  
    // 创建一个虚拟头节点,简化操作  
    ListNode dummy = new ListNode(-1);  
    ListNode current = dummy; // 当前节点  
  
    // 循环比较 l1 和 l2 的节点,将较小的节点接在当前节点后面  
    while (l1 != null && l2 != null) {  
        if (l1.val <= l2.val) {  
            current.next = l1;  
            l1 = l1.next;  
        } else {  
            current.next = l2;  
            l2 = l2.next;  
        }  
        current = current.next;  
    }  
  
    // 将剩余的节点接在当前节点后面  
    if (l1 != null) {  
        current.next = l1;  
    }  
    if (l2 != null) {  
        current.next = l2;  
    }  
  
    return dummy.next; // 返回虚拟头节点的下一个节点,即合并后的链表头节点  
}
```

## 效率

- 时间复杂度: O(m+n), 其中 m 和 n 分别是两个链表的长度。我们需要遍历两个链表的所有节点。
- 空间复杂度: O(1), 我们只使用了常数级别的额外空间。

# 24. 树的子结构

## 题目

输入两棵二叉树A和B,判断B是不是A的子结构。(约定空树不是任意一个树的子结构), B是A的子结构,即A中有出现和B相同的结构和节点值。

例如:
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^gvK94j30L8C8sMAxs1W9w|树的子结构]]

返回true,因为B与A的一个子树拥有相同的结构和节点值。

示例1:
输入: A = [1,2,3], B = [3,1]
输出: false

示例2:

## 思路

1. 首先判断 A 或 B 是否为空,如果为空直接返回 false。
2. 从 A 的根节点开始查找是否包含 B,包含则返回 true,否则递归检查 A 的左右子树。
3. 在 `dfsContains` 方法中,如果 B 为空说明已经找到了 B 在 A 中的子结构,返回 true。
4. 如果 A 为空或者 A、B 节点值不相等,说明 B 不是 A 的子结构,返回 false。
5. 否则递归检查 A 的左右子树是否包含 B 的左右子树。

**代码解释**:
1. `isSubStructure` 方法首先判断 A 或 B 是否为空,如果为空直接返回 false。
2. 然后从 A 的根节点开始调用 `dfsContains` 方法,如果返回 true 则说明 B 是 A 的子结构,直接返回 true。
3. 如果 `dfsContains` 返回 false,则继续递归检查 A 的左右子树是否包含 B。
4. `dfsContains` 方法用于递归检查 A 的子树是否包含 B 的子结构。如果 B 为空,说明已经找到了 B 在 A 中的子结构,返回 true。
5. 如果 A 为空或者 A、B 节点值不相等,说明 B 不是 A 的子结构,返回 false。
6. 否则递归检查 A 的左右子树是否包含 B 的左右子树。

## 代码

```java
public boolean isSubStructure(TreeNode A, TreeNode B) {  
    // 如果 A 或 B 为空,直接返回 false    if (A == null || B == null) {  
        return false;  
    }  
    // 从 A 的根节点开始查找是否包含 B    return dfsContains(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);  
}  
private boolean dfsContains(TreeNode A, TreeNode B) {  
    // 如果 B 为空,说明已经找到了 B 在 A 中的子结构  
    if (B == null) {  
        return true;  
    }  
    // 如果 A 为空或者 A、B 节点值不相等,说明 B 不是 A 的子结构  
    if (A == null || A.val != B.val) {  
        return false;  
    }  
    // 递归检查 A 的左右子树是否包含 B 的左右子树  
    return dfsContains(A.left, B.left) && dfsContains(A.right, B.right);  
}
```

## 效率

- 时间复杂度: O(m\*n), 其中 m 和 n 分别是树 A 和树 B 的节点数。在最坏情况下,我们需要遍历树 A 的所有节点,并对每个节点进行 `dfsContains` 操作,该操作的时间复杂度为 O(n)。
- 空间复杂度: O(m+n), 其中 m 和 n 分别是树 A 和树 B 的节点数。在最坏情况下,递归调用的深度可能达到 m+n,因此需要 O(m+n) 的空间来存储递归调用栈。

# 25. 二叉树的镜像

## 题目

请完成一个函数,输入一个二叉树,该函数输出它的镜像。

例如输入与输出:
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^IsOnA-PLvEjffQ8cdqoNO|二叉树的镜像]]

示例1:

输入: root = [4,2,7,1,3,6,9]
输出: [4,7,2,9,6,3,1]

## 思路

1. 如果根节点为空,直接返回 null。
2. 交换根节点的左右子树。
3. 递归地对左右子树进行镜像操作。
4. 返回根节点。

**代码解释**:
1. `mirrorTree` 方法首先判断根节点是否为空,如果为空直接返回 null。
2. 然后交换根节点的左右子树,使用一个临时变量 `temp` 来暂存左子树。
3. 递归地对左右子树调用 `mirrorTree` 方法,完成镜像操作。
4. 最后返回根节点。

## 代码

```java
public TreeNode mirrorTree(TreeNode root) {  
    if (root == null) {  
        return null;  
    }  
    // 交换左右子树  
    TreeNode temp = root.left;  
    root.left = mirrorTree(root.right);  
    root.right = mirrorTree(temp);  
  
    return root;  
}
```

## 效率

- 时间复杂度: O(n), 其中 n 是二叉树的节点数。我们需要遍历二叉树的所有节点,对每个节点进行镜像操作。
- 空间复杂度: O(n), 在最坏情况下,递归调用的深度达到 n,因此需要 O(n) 的空间来存储递归调用栈。

# 26. 对称的二叉树

## 题目

请实现一个函数,用来判断一棵二叉树是不是对称的。如果一棵二叉树和它  
的镜像一样,那么它是对称的。

例如,二叉树[1,2,2,3,4,4,3]是对称的。

但是二叉树[1,2,2,null,3,null,3]则不是镜像对称的:

[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^iZkU7qnzRiEnP_KB-fwAN|对称二叉树]]

示例1:

输入: root=[1,2,2,3,4,4,3]  
输出: true

示例2:
输入: root=[1,2,2,null,3,null,3]  
输出: false

## 思路

1. 如果根节点为空,直接返回 true。
2. 调用 `isMirror` 方法,比较根节点的左子树和右子树是否对称。
3. 在 `isMirror` 方法中,如果左右节点同时为空,返回 true。
4. 如果左右节点有一个为空,返回 false。
5. 比较左右节点的值是否相等,并递归比较左节点的左子树和右节点的右子树,以及左节点的右子树和右节点的左子树。

**代码解释**:

1. `isSymmetric` 方法首先判断根节点是否为空,如果为空直接返回 true。
2. 然后调用 `isMirror` 方法,比较根节点的左子树和右子树是否对称。
3. `isMirror` 方法用于递归比较左右节点是否对称。如果左右节点同时为空,返回 true。
4. 如果左右节点有一个为空,返回 false。
5. 比较左右节点的值是否相等,并递归比较左节点的左子树和右节点的右子树,以及左节点的右子树和右节点的左子树。

## 代码

```java
public boolean isSymmetric(TreeNode root) {  
    if (root == null) {  
        return true;  
    }  
    return isMirror(root.left, root.right);  
}  
  
private boolean isMirror(TreeNode left, TreeNode right) {  
    if (left == null && right == null) {  
        return true;  
    }  
    if (left == null || right == null) {  
        return false;  
    }  
    return (left.val == right.val) && isMirror(left.left, right.right) && isMirror(left.right, right.left);  
}
```

## 效率

- 时间复杂度: O(n), 其中 n 是二叉树的节点数。我们需要遍历二叉树的所有节点,对每个节点进行对称性检查。
- 空间复杂度: O(n), 在最坏情况下,递归调用的深度达到 n,因此需要 O(n) 的空间来存储递归调用栈。

# 27. 顺时针打印矩阵

## 题目

输入一个矩阵,按照从外向里以顺时针的顺序依次打印出每一个数字。

示例1:
输入: 
matrix=
[
	[1,2,3],
	[4,5,6],
	[7,8,9]
]
输出: [1,2,3,6,9,8,7,4,5]

示例2:
输入: 
matrix=
[
	[1,2,3,4],
	[5,6,7,8],
	[9,10,11,12]
]
输出:[1,2,3,4,8,12,11,10,9,5,6,7]

限制:
- 0 <= matrix.length <= 100
- 0 <= matrix[i].length <= 100

## 思路

1. 定义上下左右四个边界,初始时分别为矩阵的上下左右边界。
2. 依次按照从左到右、从上到下、从右到左、从下到上的顺序遍历矩阵,并将遍历到的数字加入结果列表中。
3. 每遍历完一个方向后,更新相应的边界。
4. 继续循环,直到遍历完所有数字。

## 代码

```java
public List<Integer> spiralOrder(int[][] matrix) {  
    List<Integer> result = new ArrayList<>();  
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {  
        return result;  
    }  
    int rows = matrix.length;  
    int cols = matrix[0].length;  
    int top = 0, bottom = rows - 1, left = 0, right = cols - 1;  
    while (top <= bottom && left <= right) {  
        // 从左到右  
        for (int i = left; i <= right; i++) {  
            result.add(matrix[top][i]);  
        }  
        top++;  
        // 从上到下  
        for (int i = top; i <= bottom; i++) {  
            result.add(matrix[i][right]);  
        }  
        right--;  
        if (top <= bottom) {  
            // 从右到左  
            for (int i = right; i >= left; i--) {  
                result.add(matrix[bottom][i]);  
            }  
            bottom--;  
        }  
        if (left <= right) {  
            // 从下到上  
            for (int i = bottom; i >= top; i--) {  
                result.add(matrix[i][left]);  
            }  
            left++;  
        }  
    }  
    return result;  
}
```

## 效率

- 时间复杂度: O(m\*n), 其中 m 为矩阵的行数, n 为矩阵的列数。我们需要遍历矩阵中的每个元素。
- 空间复杂度: O(1), 我们只需要常数级别的额外空间来存储边界和遍历过程中的临时变量。

# 28. 包含min函数的栈

## 题目

定义栈的数据结构,请在该类型中实现一个能够得到栈的最小元素的min函数在该栈中,调用min、push及pop的时间复杂度都是O(1)。

示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();  --> 返回 -3.
minStack.pop();
minStack.top();  --> 返回 0.
minStack.min();  --> 返回 -2.

提示: 各函数的调用总次数不超过20000次

## 思路

- 使用两个栈，一个用来存储数据（stack），另一个用来存储最小值（minStack）。
- 在push操作时，如果当前值小于等于minStack的栈顶元素，就将当前值也压入minStack中，以保证minStack的栈顶始终是最小值。
- 在pop操作时，如果stack弹出的元素等于minStack的栈顶元素，也将minStack的栈顶元素弹出，以保证minStack的栈顶始终是当前栈中的最小值。

## 代码

```java
class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }
    public void pop() {
        if (stack.pop().equals(minStack.peek())) {
            minStack.pop();
        }
    }
    public int top() {
        return stack.peek();
    }
    public int min() {
        return minStack.peek();
    }
}
```

## 效率

- 时间复杂度：push、pop、top、min操作的时间复杂度都是O(1)。
- 空间复杂度：O(n)，其中n为栈中元素的个数。

# 29. 栈的压入、弹出序列

## 题目

输入两个整数序列,第一个序列表示栈的压入顺序,请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如,序列{1,2,3,4,5}是某栈的压栈序列,序列{4,5,3,2,1}是该压栈序列对应的一个弹出序列,但{4,3,5,1,2}就不可能是该压栈序列的弹出序列。

示例1:
输入: pushed=[1,2,3,4,5], popped= [4,5,3,2,1]
输出: true
解释: 我们可以按以下顺序执行:
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

示例2:
输入: pushed=[1,2,3,4,5], popped= [4,3,5,1,2]
输出: false
解释: 1 不能在 2 之前弹出。


## 思路

- 使用一个辅助栈来模拟入栈和出栈操作。
- 遍历压栈序列，将元素依次入栈，每次入栈后检查栈顶元素是否与弹出序列的当前元素相同，如果相同则执行出栈操作。
- 最后检查辅助栈是否为空，如果为空则说明弹出序列是合法的。

**代码分析：**
1. 首先创建一个Stack对象stack，用于模拟栈的操作。
2. 使用变量i来追踪弹出序列popped的索引，初始值为0。
3. 遍历压栈序列pushed，对于其中的每个元素num，执行以下操作：
    - 将num入栈，模拟入栈操作。
    - 然后检查栈顶元素是否与弹出序列的当前元素popped[i]相同，如果相同则执行出栈操作并递增i，直到栈顶元素与popped[i]不相同为止。
4. 最后检查辅助栈是否为空，如果为空则说明弹出序列是合法的，返回true；否则返回false

## 代码

```java
public boolean validateStackSequences(int[] pushed, int[] popped) {  
    Stack<Integer> stack = new Stack<>();  
    int i = 0;  
    for (int num : pushed) {  
        stack.push(num); // 模拟入栈操作  
        while (!stack.isEmpty() && stack.peek() == popped[i]) {  
            stack.pop(); // 模拟出栈操作  
            i++;  
        }  
    }  
    return stack.isEmpty();  
}
```

## 效率

- 时间复杂度：O(n)，其中n为pushed和popped的长度，需要遍历一次pushed和popped数组。
- 空间复杂度：O(n)，使用了一个辅助栈来模拟入栈和出栈操作。

# 30. 从上到下打印二叉树 Ⅰ

## 题目

从上到下打印出二叉树的每个节点,同一层的节点按照从左到右的顺序打
印。

例如:
给定二叉树:[3,9,20,null,null,15,7],

[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^GrPhnsVO3VCleXkM21FwH|从上到下打印二叉树]]

返回:
[3,9,20,15,7]

提示: 节点总数 <= 1000

## 思路

- 使用队列进行层序遍历，首先将根节点加入队列，然后循环处理队列中的节点，依次将它们的值加入结果列表，并将它们的子节点加入队列。
- 循环直到队列为空。

**代码分析：**
- 在Solution类中，定义了一个levelOrder方法，用于实现二叉树的层序遍历。
- 在levelOrder方法中，使用队列来进行层序遍历，首先将根节点加入队列，然后在循环中依次取出队列中的节点，将其值加入结果列表，并将其左右子节点加入队列。
- 最后返回结果列表。

## 代码

```java
public List<Integer> levelOrder(TreeNode root) {  
    List<Integer> result = new ArrayList<>();  
    if (root == null) {  
        return result;  
    }  
  
    Queue<TreeNode> queue = new LinkedList<>();  
    queue.offer(root);  
  
    while (!queue.isEmpty()) {  
        int levelSize = queue.size();  
        for (int i = 0; i < levelSize; i++) {  
            TreeNode node = queue.poll();  
            result.add(node.val);  
            if (node.left != null) {  
                queue.offer(node.left);  
            }  
            if (node.right != null) {  
                queue.offer(node.right);  
            }  
        }  
    }  
  
    return result;  
}
```

## 效率

- 时间复杂度为O(n)，其中n为树的节点数，因为需要遍历每个节点。
- 空间复杂度为O(n)，最坏情况下队列中会存储树的所有叶子节点，所以空间复杂度为O(n)

# 31. 打印二叉树 Ⅱ

## 题目

从上到下按层打印二叉树,同一层的节点按从左到右的顺序打印,每一层打印到一行。

例如:
给定二叉树: [3,9,20,null,null,15,7]

[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^GrPhnsVO3VCleXkM21FwH|打印二叉树]]

返回其层次遍历结果:
[
	[3],
	[9,20],
	[15,7]
]

## 思路

- 使用队列进行层次遍历，类似于上一个问题的解决方案。
- 在遍历每一层时，将该层的节点值加入一个临时列表，然后将该列表加入结果列表。
- 循环直到队列为空。

**代码分析**：
- 在Solution类中，定义了一个levelOrder方法，用于实现二叉树的层次遍历并按层打印。
- 在levelOrder方法中，使用队列进行层次遍历，每遍历完一层时，将该层的节点值列表加入结果列表。
- 最后返回包含每一层节点值列表的结果列表。

## 代码

```java
public List<List<Integer>> levelOrder(TreeNode root) {  
    List<List<Integer>> result = new ArrayList<>();  
    if (root == null) {  
        return result;  
    }  
  
    Queue<TreeNode> queue = new LinkedList<>();  
    queue.offer(root);  
  
    while (!queue.isEmpty()) {  
        int levelSize = queue.size();  
        List<Integer> levelNodes = new ArrayList<>();  
        for (int i = 0; i < levelSize; i++) {  
            TreeNode node = queue.poll();  
            levelNodes.add(node.val);  
            if (node.left != null) {  
                queue.offer(node.left);  
            }  
            if (node.right != null) {  
                queue.offer(node.right);  
            }  
        }  
        result.add(levelNodes);  
    }  
  
    return result;  
}
```

## 效率

- 时间复杂度为O(n)，其中n为树的节点数，因为需要遍历每个节点。
- 空间复杂度为O(n)，最坏情况下队列中会存储树的所有叶子节点，所以空间复杂度为O(n)。

# 32. 打印二叉树 Ⅲ

## 题目

请实现一个函数按照之字形顺序打印二叉树, 即第一行按照从左到右的顺序打印, 第二层按照从右到左的顺序打印,第三行再按照从左到右的顺序打印, 其他行以此类推。

例如:
给定二叉树:[3,9,20,null,null,15,7],
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^GrPhnsVO3VCleXkM21FwH|打印二叉树]]

返回其层次遍历结果:
[
	[3],
	[20,9],
	[15,7]
]

## 思路

- 类似于层次遍历，但在遍历每一层时需要判断打印顺序。
- 使用一个布尔变量来控制每一层的打印顺序。
- 在遍历每一层时，根据布尔变量的值决定是直接加入列表还是先压入栈再加入列表。

**代码分析：**
- 在Solution类中，定义了一个zigzagLevelOrder方法，用于实现按之字形顺序打印二叉树。
- 在zigzagLevelOrder方法中，使用队列进行层次遍历，并使用一个布尔变量leftToRight来控制每一层的打印顺序。
- 在遍历每一层时，如果是从左到右的顺序，则直接将节点值加入列表；如果是从右到左的顺序，则将节点值先压入栈，再依次弹出加入列表。
- 最后返回包含每一层节点值列表的结果列表。

## 代码

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {  
    List<List<Integer>> result = new ArrayList<>();  
    if (root == null) {  
        return result;  
    }  
  
    Queue<TreeNode> queue = new LinkedList<>();  
    queue.offer(root);  
    boolean leftToRight = true;  
  
    while (!queue.isEmpty()) {  
        int levelSize = queue.size();  
        List<Integer> levelNodes = new ArrayList<>();  
        Stack<Integer> levelStack = new Stack<>();  
  
        for (int i = 0; i < levelSize; i++) {  
            TreeNode node = queue.poll();  
            if (leftToRight) {  
                levelNodes.add(node.val);  
            } else {  
                levelStack.push(node.val);  
            }  
            if (node.left != null) {  
                queue.offer(node.left);  
            }  
            if (node.right != null) {  
                queue.offer(node.right);  
            }  
        }  
        while (!levelStack.isEmpty()) {  
            levelNodes.add(levelStack.pop());  
        }  
        result.add(levelNodes);  
        leftToRight = !leftToRight;  
    }  
    return result;  
}
```

## 效率

- 时间复杂度为O(n)，其中n为树的节点数，因为需要遍历每个节点。
- 空间复杂度为O(n)，最坏情况下队列中会存储树的所有叶子节点，所以空间复杂度为O(n)。

# 33. 二叉搜索树的后序遍历序列

## 题目

输入一个整数数组,判断该数组是不是某二叉搜索树的后序遍历结果。如果
是则返回 true,否则返回 false。假设输入的数组的任意两个数字都
互不相同。

参考以下这颗二叉搜索树:


示例1:
输入: [1,6,3,2,5]
输出: false

示例2:
输入: [1,3,2,6,5]
输出: true

## 思路

- 后序遍历的顺序是左子树 -> 右子树 -> 根节点，对于二叉搜索树，左子树的节点值都小于根节点，右子树的节点值都大于根节点。
- 根据这个特点，可以通过递归判断每个子树是否符合二叉搜索树的条件。

**代码分析：**
- 在Solution类中，定义了一个verifyPostorder方法用于判断输入整数数组是否为某二叉搜索树的后序遍历结果。
- 在verifyPostorder方法中，使用递归来判断是否满足二叉搜索树的条件。
- 在每次递归中，找到根节点，然后判断左子树和右子树是否满足二叉搜索树的条件。

## 代码

```java
public boolean verifyPostorder(int[] postorder) {  
    if (postorder == null || postorder.length == 0) {  
        return false;  
    }  
  
    return verifyPostorder(postorder, 0, postorder.length - 1);  
}  
  
private boolean verifyPostorder(int[] postorder, int start, int end) {  
    if (start >= end) {  
        return true;  
    }  
  
    int rootVal = postorder[end];  
    int i = start;  
    while (postorder[i] < rootVal) {  
        i++;  
    }  
  
    int j = i;  
    while (postorder[j] > rootVal) {  
        j++;  
    }  
  
    return j == end && verifyPostorder(postorder, start, i - 1) && verifyPostorder(postorder, i, end - 1);  
}
```

## 效率

- 时间复杂度为O(nlogn)，其中n为数组的长度，因为每次递归都需要遍历一部分数组。
- 空间复杂度为O(logn)，递归调用栈的深度取决于树的高度，最坏情况下为O(n)。

# 34. 二叉树中和为某一值的路径

## 题目

给你二叉树的根节点 root 和一个整数目标和 targetSum,找出所有从根节点到叶子节点 路径总和等于给定目标和的路径。叶子节点 是指没有子节点的节点。

示例1:
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^3Iyw-3kpbAM2MRT4eJ4EK|题目]]

输入:
root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出:
[
	[5,4,11,2],
	[5,8, 4,5]
]

## 思路

- 使用深度优先搜索（DFS）来遍历二叉树，同时记录路径上的节点值。
- 当遍历到叶子节点时，判断路径总和是否等于给定目标和，如果是则将路径加入结果列表中。

**代码分析：**
- 在Solution类中，定义了一个pathSum方法用于找出路径总和等于给定目标和的路径。
- 在findPaths方法中，使用递归来遍历二叉树，并查找满足条件的路径。
- 每次递归中，将当前节点值加入路径列表中，并判断是否为叶子节点且路径总和等于目标和。

## 代码

```java
public List<List<Integer>> pathSum(TreeNode root, int targetSum) {  
    List<List<Integer>> result = new ArrayList<>();  
    List<Integer> path = new ArrayList<>();  
    findPaths(root, targetSum, result, path);  
    return result;  
}
```

## 效率

- 时间复杂度为O(n)，其中n为二叉树中的节点数，需要遍历每个节点。
- 空间复杂度为O(n)，递归调用栈的深度取决于树的高度，最坏情况下为O(n)。此外，需要额外的空间来存储路径列表。

# 35. 复杂链表的复制

## 题目

请实现 copyRandomList 函数,复制一个复杂链表。在复杂链表中,每个节点除了有一个 next 指针指向下一个节点,还有一个random 指针指向链表中的任意节点或者 null。

示例1:
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^bm6FIt1S|示例1图示]]

输入: head = [\[7,null],[13,0],[11,4],[10,2],[1,0]]
输出: [\[7,null],[13,0],[11,4],[10,2],[1,0]]

示例2:
[[Excalidraw/Draw 2024-05-08_21.excalidraw.md#^JGNqGlUH|示例2图示]]

输入: head = [\[1,1],[2,1]]
输出: [\[1,1],[2,1]]

## 思路

1. 通过在原链表上插入新节点的方式来创建新链表,这样可以保持原链表的结构不变。
2. 利用原链表的random指针来设置新链表节点的random指针。
3. 最后分离原链表和新链表。

**代码分析:**
1. 第一步: 创建新节点并将其插入到原节点之后。这样可以保持原节点的random指针不变,并且新节点的next指针也能正确指向下一个节点。
2. 第二步: 设置新节点的random指针。由于新节点已经插入到原节点之后,我们可以通过原节点的random指针来设置新节点的random指针。
3. 第三步: 分离原链表和新链表。通过遍历原链表,将原链表和新链表分离开来。

## 代码

```java
public Node copyRandomList(Node head) {  
    if (head == null) {  
        return null;  
    }  
  
    // Step 1: Create new nodes and link them to the original nodes  
    Node current = head;  
    while (current != null) {  
        Node newNode = new Node(current.val);  
        newNode.next = current.next;  
        current.next = newNode;  
        current = newNode.next;  
    }  
  
    // Step 2: Set the random pointers for the new nodes  
    current = head;  
    while (current != null) {  
        if (current.random != null) {  
            current.next.random = current.random.next;  
        }  
        current = current.next.next;  
    }  
  
    // Step 3: Separate the original and copied lists  
    current = head;  
    Node newHead = head.next;  
    while (current != null) {  
        Node temp = current.next;  
        current.next = temp.next;  
        if (temp.next != null) {  
            temp.next = temp.next.next;  
        }  
        current = current.next;  
    }  
  
    return newHead;  
}
```

## 效率

- 时间复杂度为O(n),其中n为链表中的节点数。我们需要遍历链表三次。
- 空间复杂度为O(1),我们只使用了常量级的额外空间来存储临时变量。

# 36. 二叉搜索树与双向链表

## 题目

输入一棵二叉搜索树,将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点,只能调整树中节点指针的指向。

为了让您更好地理解问题,以下面的二叉搜索树为例:
		4
	2       5
1       3
我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表,第一个节点的前驱是最后一个节点, 最后一个节点的后继是第一个节点。"head"表示指向链表中有最小元素的节点。

特别地,我们希望可以就地完成转换操作。当转化完成以后,树中节点的左指针需要指向前驱,树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

## 思路

思路:

1. 使用中序遍历遍历二叉搜索树，同时修改节点的指针指向，使其成为双向链表。
2. 在中序遍历的过程中，记录前一个节点prev和头节点head，最后将头尾相连，形成循环双向链表。

**代码分析:**

- 在Solution类中，定义了一个treeToDoublyList方法用于将二叉搜索树转换为排序的循环双向链表。
- 使用中序遍历来遍历二叉搜索树，并在遍历的过程中修改节点指针的指向。
- 最后，将头尾相连，形成循环双向链表。

## 代码

```java
public CircleNode treeToDoublyList(CircleNode root) {  
    if (root == null) {  
        return null;  
    }  
  
    prev = null;  
    head = null;  
  
    inorderTraversal(root);  
  
    // Connect head and tail to make it a circular doubly linked list  
    head.left = prev;  
    prev.right = head;  
  
    return head;  
}  
  
private void inorderTraversal(CircleNode node) {  
    if (node != null) {  
        inorderTraversal(node.left);  
  
        if (prev == null) {  
            head = node; // Set head if it's the first node  
        } else {  
            prev.right = node;  
            node.left = prev;  
        }  
  
        prev = node; // Update prev to the current node  
        inorderTraversal(node.right);  
    }  
}
```

## 效率

- 时间复杂度为O(n)，其中n为二叉搜索树中的节点数，需要遍历所有节点。
- 空间复杂度为O(1)，没有使用额外的数据结构，只使用了常量级的额外空间来存储临时变量。

# 37. 序列化二叉树

## 题目

请实现两个函数,分别用来序列化和反序列化二叉树。

你需要设计一个算法来实现二叉树的序列此与反序列化。这里不限定你的序列/反序列化算法执行逻辑,你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

示例1：
	1
2        3
	4        5

输入: root = [1,2,3,null,null,4,5] 
输出: [1,2,3,null,null,4,5]

## 思路

1. 序列化：采用前序遍历的方式将二叉树序列化为字符串，使用逗号分隔节点值，空节点用字符串"null"表示。
2. 反序列化：根据序列化后的字符串，利用递归的方式逐步构建二叉树的左右子树，直至还原整个二叉树。

**代码分析:**
- Codec类中包含了serialize和deserialize两个方法，分别用于序列化和反序列化二叉树。
- 在serialize方法中，采用前序遍历的方式将二叉树序列化为字符串。
- 在deserialize方法中，通过递归方式将序列化后的字符串反序列化为原始的二叉树。

## 代码

```java
// Encodes a tree to a single string.  
public String serialize(TreeNode root) {  
    if (root == null) {  
        return "null";  
    }  
  
    String leftSerialized = serialize(root.left);  
    String rightSerialized = serialize(root.right);  
  
    return root.val + "," + leftSerialized + "," + rightSerialized;  
}  
  
// Decodes your encoded data to tree.  
public TreeNode deserialize(String data) {  
    Queue<String> nodes = new LinkedList<>(Arrays.asList(data.split(",")));  
    return deserializeHelper(nodes);  
}  
  
private TreeNode deserializeHelper(Queue<String> nodes) {  
    String val = nodes.poll();  
    if (val.equals("null")) {  
        return null;  
    }  
  
    TreeNode node = new TreeNode(Integer.parseInt(val));  
    node.left = deserializeHelper(nodes);  
    node.right = deserializeHelper(nodes);  
  
    return node;  
}
```

## 效率

- 序列化时间复杂度为O(n)，其中n为二叉树中的节点数，需要遍历所有节点。
- 反序列化时间复杂度为O(n)，需要递归处理所有节点。
- 空间复杂度为O(n)，用于存储序列化后的字符串和递归调用栈。

# 38. 字符串的排列

## 题目

输入一个字符串,打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组,但里面不能有重复元素。

示例:
输入: s = "abc"
输出: ["abc","acb", "bac","bca","cab","cba"]

限制: 1 <= s 的长度 <= 8

## 思路

1. 对输入字符串进行排序，以便后续剪枝操作。
2. 使用回溯算法，递归生成所有可能的排列组合。
3. 在递归过程中，使用visited数组标记字符是否已经被访问，避免重复排列的生成。

**代码分析:**
- Solution类中包含了permutation方法，用于获取输入字符串中字符的所有排列。
- 使用回溯算法实现排列的生成，通过递归实现所有可能的排列组合。
- 使用visited数组来标记字符是否已经被访问，以避免重复排列的生成。
- 使用StringBuilder来构建排列结果。

## 代码

```java
public String[] permutation(String s) {  
    List<String> result = new ArrayList<>();  
    char[] charArray = s.toCharArray();  
    boolean[] visited = new boolean[s.length()];  
    StringBuilder path = new StringBuilder();  
  
    // 对输入字符串进行排序，以便后续剪枝操作  
    Arrays.sort(charArray);  
  
    backtrack(charArray, visited, path, result);  
  
    return result.toArray(new String[0]);  
}  
  
private void backtrack(char[] charArray, boolean[] visited, StringBuilder path, List<String> result) {  
    if (path.length() == charArray.length) {  
        result.add(path.toString());  
        return;    }  
  
    for (int i = 0; i < charArray.length; i++) {  
        if (visited[i] || (i > 0 && charArray[i] == charArray[i - 1] && !visited[i - 1])) {  
            continue; // 已经访问过或者与前一个字符相同且前一个字符未被访问，则跳过  
        }  
        visited[i] = true;  
        path.append(charArray[i]);  
        backtrack(charArray, visited, path, result);  
        path.deleteCharAt(path.length() - 1);  
        visited[i] = false;  
    }  
}
```

## 效率

- 时间复杂度：O(n\*n!)，其中n为字符串的长度，n!为所有可能的排列组合数，每个排列需要O(n)的时间来构建。
- 空间复杂度：O(n\*n!)，存储所有可能的排列组合。

# 39. 数组中出现次数超过一半的数字

## 题目

数组中有一个数字出现的次数超过数组长度的一半,请找出这个数字。你可以假设数组是非空的,并且给定的数组总是存在多数元素。

示例1:
输入: [1,2,3,2,2,2,5,4,2]
输出: 2

限制: 1 <= 数组长度 <= 50000

## 思路

1. 初始化候选元素为null，初始化计数器count为0。
2. 遍历数组，对于每个元素：
    - 如果计数器count为0，则将当前元素设为候选元素。
    - 如果当前元素与候选元素相同，则计数器加1，否则计数器减1。
3. 最终得到的候选元素即为出现次数超过一半的数字。

**代码分析:**
- Solution类中包含了majorityElement方法，用于找出数组中出现次数超过一半的数字。
- 使用Boyer-Moore投票算法，遍历数组并记录候选元素以及其出现次数，最终得到出现次数超过一半的候选元素。

## 代码

```java
public int majorityElement(int[] nums) {  
    int count = 0;  
    Integer candidate = null;  
  
    for (int num : nums) {  
        if (count == 0) {  
            candidate = num;  
        }  
        count += (num == candidate) ? 1 : -1;  
    }  
  
    return candidate;  
}
```

## 效率

- 时间复杂度：O(n)，其中n为数组的长度，需要遍历整个数组。
- 空间复杂度：O(1)，只需要常数级别的额外空间。

# 40. 最小的k个数

## 题目

输入整数数组 arr,找出其中最小的k 个数。例如,输入4、5、1、6、2、7、3、8这8个数字,则最小的4个数字是1、2、3、4。

示例1:
输入: arr = [3,2,1], k = 2
输出: [1,2] 或者 [2,1]

示例2:
输入: arr = [0,1,2,1], k = 1
输出: [0]

限制:
- 0 <= k <= arr.length <= 10000
- 0 <= arr[i] <= 10000

## 思路

1. 利用快速排序的Partition操作，找到第k个最小的数。
2. 将数组划分为两部分，一部分是前k个最小的数，另一部分是比第k个数大的数。
3. 返回前k个最小的数即可。

**代码分析:**
- Solution类中包含了getLeastNumbers方法，用于找出整数数组中最小的k个数。
- 使用快速排序的Partition操作，找到第k个最小的数。

## 代码

```java
public int[] getLeastNumbers(int[] arr, int k) {  
    if (k == 0 || arr.length == 0) {  
        return new int[0];  
    }  
  
    // 使用快速排序的Partition操作，找到第k个最小的数  
    return quickSort(arr, 0, arr.length - 1, k - 1);  
}  
  
private int[] quickSort(int[] arr, int lo, int hi, int k) {  
    int j = partition(arr, lo, hi);  
    if (j == k) {  
        return Arrays.copyOf(arr, k + 1);  
    }  
    return j > k ? quickSort(arr, lo, j - 1, k) : quickSort(arr, j + 1, hi, k);  
}  
  
private int partition(int[] arr, int lo, int hi) {  
    int pivot = arr[lo];  
    int i = lo, j = hi + 1;  
    while (true) {  
        while (++i < hi && arr[i] < pivot) ;  
        while (--j > lo && arr[j] > pivot) ;  
        if (i >= j) {  
            break;  
        }  
        int temp = arr[i];  
        arr[i] = arr[j];  
        arr[j] = temp;  
    }  
    arr[lo] = arr[j];  
    arr[j] = pivot;  
    return j;  
}
```

## 效率

- 时间复杂度：O(n)，其中n为数组的长度，快速排序的Partition操作平均时间复杂度为O(n)。
- 空间复杂度：O(logn)，快速排序的递归调用栈的最大深度为O(logn)。

# 41. 数据流中的中位数

## 题目

如何得到一个数据流中的中位数? 如果从数据流中读出奇数个数值, 那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值, 那么中位数就是所有数值排序之后中间两个数的平均值。

例如, [2,3,4]的中位数是3, [2,3]的中位数是(2+3)/2=2.5

设计一个支持以下两种操作的数据结构:
- void addNum(int num) --> 从数据流中添加一个整数到数据结构中。
- double findMedian()  --> 返回目前所有元素的中位数。

示例 1：
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
\[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]

示例 2：
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
\[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]

提示：
- 最多会对 `addNum、findMedian` 进行 `50000` 次调用。

示例2:

## 思路

1. 使用两个优先队列，一个大顶堆maxHeap和一个小顶堆minHeap。
2. 当添加新元素时，如果maxHeap为空或者新元素小于等于maxHeap的堆顶，则将新元素加入maxHeap；否则将新元素加入minHeap。
3. 调整两个堆的大小，使得两个堆的大小差不超过1。
4. 获取中位数时，如果两个堆的大小相等，取两个堆顶元素的平均值作为中位数；如果maxHeap的大小大于minHeap的大小，则maxHeap的堆顶即为中位数。

**代码分析:**
- MedianFinder类实现了数据流中的中位数问题，使用了两个优先队列（堆）来存放数据流中的数。
- addNum方法用于向数据结构中添加一个整数，findMedian方法用于返回目前所有元素的中位数。

## 代码

```java
private PriorityQueue<Integer> maxHeap; // 存放数据流中较小的一半数  
private PriorityQueue<Integer> minHeap; // 存放数据流中较大的一半数  
  
/** initialize your data structure here. */  
public Solution_41() {  
    maxHeap = new PriorityQueue<>((a, b) -> b - a); // 大顶堆，存放较小的一半数，堆顶为最大值  
    minHeap = new PriorityQueue<>(); // 小顶堆，存放较大的一半数，堆顶为最小值  
}  
  
public void addNum(int num) {  
    if (maxHeap.isEmpty() || num <= maxHeap.peek()) {  
        maxHeap.offer(num);  
    } else {  
        minHeap.offer(num);  
    }  
  
    // 调整两个堆的大小，使得两个堆的大小差不超过1  
    if (maxHeap.size() > minHeap.size() + 1) {  
        minHeap.offer(maxHeap.poll());  
    } else if (minHeap.size() > maxHeap.size()) {  
        maxHeap.offer(minHeap.poll());  
    }  
}
```

## 效率

- 时间复杂度：addNum操作为O(logn)，findMedian操作为O(1)，其中n为数据流中元素的个数。
- 空间复杂度：O(n)，需要两个优先队列来存放数据流中的元素。

# 42. 连续子数组的最大和

## 题目

给你一个整数数组 nums ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
子数组是数组中的一个连续部分。  

示例 1：  
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]  
输出：6  
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。  

示例 2：  
输入：nums = [1]  
输出：1  

示例 3：  
输入：nums = [5,4,-1,7,8]  
输出：23  


提示：  
- 1 <= nums.length <= 105  
- -104 <= nums[i] <= 104

## 思路

**代码分析:**

- Solution类中包含了maxSubArray方法，用于找出具有最大和的连续子数组。
- 使用动态规划的思想，遍历数组，计算当前和和最大和。

**思路:**

1. 使用动态规划的思想，遍历数组，计算当前和和最大和。
2. 对于每个元素，计算以该元素结尾的最大和的子数组，同时更新最大和。

## 代码

```java
public int maxSubArray(int[] nums) {  
    int maxSum = nums[0]; // 最大和初始值为数组的第一个元素  
    int currentSum = nums[0]; // 当前和初始值为数组的第一个元素  
  
    for (int i = 1; i < nums.length; i++) {  
        // 计算当前和，如果当前和小于当前元素，则从当前元素重新开始计算当前和  
        currentSum = Math.max(nums[i], currentSum + nums[i]);  
        // 更新最大和  
        maxSum = Math.max(maxSum, currentSum);  
    }  
  
    return maxSum;  
}
```

## 效率

- 时间复杂度：O(n)，其中n为数组的长度，只需要遍历一次数组。
- 空间复杂度：O(1)，只需要常数级别的额外空间。

# 43. 1 ~ n 整数中1出现的次数

## 题目

输入一个整数 n,求1~n这n个整数的十进制表示中1出现的次数。

例如,输入12, 1 ~ 12这些整数中包含1的数字有1、10、11和12, 1一共出现了5次。

示例1:
输入: n = 12
输出: 5

示例2:
输入: n = 13
输出: 6

限制: 1 <= n < 2^31

## 思路

**代码分析:**
- Solution类中包含了countDigitOne方法，用于计算1~n这n个整数的十进制表示中1出现的次数。
- 在循环中，对于每个i（1, 10, 100, 1000, ...），计算1在每个位上出现的次数，并累加到count中。

**思路:**
1. 遍历每个数位，分别计算每个数位上1出现的次数，并累加到count中。
2. 对于每个数位i（1, 10, 100, 1000, ...），计算1在每个位上出现的次数，然后累加到count中。

## 代码

```java
public int countDigitOne(int n) {  
    int count = 0;  
    for (long i = 1; i <= n; i *= 10) {  
        long divider = i * 10;  
        count += (n / divider) * i + Math.min(Math.max(n % divider - i + 1, 0), i);  
    }  
    return count;  
}
```

## 效率

- 时间复杂度：O(logn)，其中n为输入的整数，需要遍历整数的位数。
- 空间复杂度：O(1)，只需要常数级别的额外空间。

# 44. 数字序列中某一位的数字

## 题目

数字以0123456789101112131415...的格式序列化到一个字符序列中。在这个序列中,第5位(从下标0开始计数)是5, 第13位是1，第19位是4, 等等。

请写一个函数,求任意第n位对应的数字。

示例1: 
输入: n = 3
输出: 3

示例2: 
输入: n = 11
输出: 0

限制: 0 <= n < 2^31

## 思路

**代码分析:**
- Solution类中包含了findNthDigit方法，用于求任意第n位对应的数字。
- 通过计算确定n所在的数字的位数范围，然后确定n所在的数字，最后确定n所在数字的哪一位。

**思路:**
1. 确定n所在的数字的位数范围。
2. 确定n所在的数字。
3. 确定n所在数字的哪一位。

## 代码

```java
public int findNthDigit(int n) {  
    // 位数，初始为一位数  
    int digit = 1;  
    // 起始数字，初始为1  
    long start = 1;  
    // 数字范围内的数字个数，初始为9  
    long count = 9;  
  
    // 确定n所在的数字的位数范围  
    while (n > digit * count) {  
        n -= digit * count;  
        digit++;  
        start *= 10;  
        count = 9 * start * digit;  
    }  
  
    // 确定n所在的数字  
    long num = start + (n - 1) / digit;  
    // 确定n所在数字的哪一位  
    return String.valueOf(num).charAt((n - 1) % digit) - '0';  
}
```

## 效率

- 时间复杂度：O(logn)，其中n为输入的整数，需要遍历整数的位数。
- 空间复杂度：O(1)，只需要常数级别的额外空间。

# ！45. 把数组排成最小的数

## 题目



## 思路

**代码分析:**
- Solution类中包含了minNumber方法，用于将给定数组排成最小的数。
- 将整数数组转换为字符串数组，然后使用自定义的比较器进行排序，最后将排序后的字符串数组拼接成最小的数。

**思路:**
1. 将整数数组转换为字符串数组。
2. 自定义排序规则，对字符串数组进行排序，排序规则为将两个字符串拼接后比较大小。
3. 将排序后的字符串数组拼接成最小的数。

## 代码

```java
public String minNumber(int[] nums) {  
    // 将整数数组转换为字符串数组  
    String[] numStrs = new String[nums.length];  
    for (int i = 0; i < nums.length; i++) {  
        numStrs[i] = String.valueOf(nums[i]);  
    }  
  
    // 自定义排序规则  
    Arrays.sort(numStrs, new Comparator<String>() {  
        @Override  
        public int compare(String a, String b) {  
            String order1 = a + b;  
            String order2 = b + a;  
            return order1.compareTo(order2);  
        }  
    });  
  
    // 将排序后的字符串数组拼接成最小的数  
    StringBuilder result = new StringBuilder();  
    for (String numStr : numStrs) {  
        result.append(numStr);  
    }  
  
    return result.toString();  
}
```

## 效率

- 时间复杂度：O(nlogn)，其中n为数组的长度，主要消耗在排序操作上。
- 空间复杂度：O(n)，需要额外的字符串数组来存储转换后的数字。

# 46. 把数字翻译成字符串

## 题目

给定一个数字,我们按照如下规则把它翻译为字符串: 0翻译成"a", 1翻译成"b" ... 11翻译成"l" ... 25翻译成"z"。
一个数字可能有多个翻译。请编程实现一个函数, 用来计算一个数字有多少种不同的翻译方法。


示例 1:
输入: 12258
输出: 5
解释: 12258有5种不同的翻译,分别是“bccfi","bwfi","bczi","mcfi"和"mzi"

提示: 0 <= num < 231

## 思路

**代码分析:**
- translateNum方法用于计算一个数字有多少种不同的翻译方法。
- 使用动态规划来解决问题，dp[i]表示以第i位结尾的数字的翻译方法数量。
- 根据题目规则，判断当前数字和前一位数字组成的两位数是否在翻译范围内，然后更新dp数组。

**思路:**
1. 将输入的数字转换为字符串，方便处理。
2. 使用动态规划，定义dp数组，dp[i]表示以第i位结尾的数字的翻译方法数量。
3. 遍历数字的每一位，根据题目规则判断当前数字和前一位数字组成的两位数是否在翻译范围内，然后更新dp数组。
4. 返回dp数组的最后一个元素即为结果。

## 代码

```java
public int translateNum(int num) {  
    String numStr = String.valueOf(num);  
    int len = numStr.length();  
    int[] dp = new int[len + 1];  
    dp[0] = 1;  
    dp[1] = 1;  
  
    for (int i = 2; i <= len; i++) {  
        String twoDigits = numStr.substring(i - 2, i);  
        if (twoDigits.compareTo("10") >= 0 && twoDigits.compareTo("25") <= 0) {  
            dp[i] = dp[i - 1] + dp[i - 2];  
        } else {  
            dp[i] = dp[i - 1];  
        }  
    }  
  
    return dp[len];  
}
```

## 效率

- 时间复杂度：O(n)，其中n为输入数字的位数，需要遍历每一位数字。
- 空间复杂度：O(n)，需要额外的dp数组来存储中间结果。

# 47. 礼物的最大价值

## 题目

在一个m\*n的棋盘的每一格都放有一个礼物, 每个礼物都有一定的价值(价值大于0)。你可以从棋盘的左上角开始拿格子里的礼物, 并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值, 请计算你最多能拿到多少价值的礼物?

示例1:
输入:
[
	[1,3,1],
	[1,5,1],
	[4,2,1]
]
输出: 12
解释: 路径 1→3-5-2→1 可以拿到最多价值的礼物

提示:
- 0 < grid.length <= 200
- 0 < grid[0].length <= 200

## 思路

**代码分析:**
- Solution类中包含了maxValue方法，用于计算最多能拿到的价值。
- 使用动态规划来解决问题，dp[i][j]表示到达第i行第j列格子时的最大价值。
- 初始化第一行和第一列的最大价值，然后逐行逐列计算每个位置的最大价值。

**思路:**
1. 定义一个二维数组dp，dp[i][j]表示到达第i行第j列格子时的最大价值。
2. 初始化第一行和第一列的最大价值，dp[0][j]表示第一行的最大价值，dp[i][0]表示第一列的最大价值。
3. 从第二行第二列开始，计算每个位置的最大价值，dp[i][j]等于上方格子和左方格子中的较大值加上当前格子的价值。
4. 返回dp[m-1][n-1]即为最终的最大价值。

## 代码

```java
public int maxValue(int[][] grid) {  
    int m = grid.length;  
    int n = grid[0].length;  
    int[][] dp = new int[m][n];  
    dp[0][0] = grid[0][0];  
  
    // 初始化第一行和第一列的最大价值  
    for (int i = 1; i < m; i++) {  
        dp[i][0] = dp[i - 1][0] + grid[i][0];  
    }  
    for (int j = 1; j < n; j++) {  
        dp[0][j] = dp[0][j - 1] + grid[0][j];  
    }  
  
    // 计算每个位置的最大价值  
    for (int i = 1; i < m; i++) {  
        for (int j = 1; j < n; j++) {  
            dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];  
        }  
    }  
  
    return dp[m - 1][n - 1];  
}
```

## 效率

- 时间复杂度：O(m\*n)，其中m为棋盘的行数，n为棋盘的列数，需要遍历每个格子。
- 空间复杂度：O(m\*n)，需要额外的二维数组dp来存储中间结果。

# 48. 最长不含重复字符的子字符串

## 题目

请从字符串中找出一个最长的不包含重氧字符的子字符串,计算该最长子字符串的长度。

示例1:
输入: "abcabcbb"
输出:  3
解释: 因为无重复字符的最长子串是“abc", 所以其长度为 3。

示例2:
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是“b",所以其长度为 1。

示例3:
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是“wke", 所以其长度为 3。请注意,你的答案必须是 子串 的长度, "pwke"是一个子序列, 不是子串。

## 思路

1. 使用一个哈希表(Map)来存储每个字符及其最后一次出现的位置。
2. 遍历字符串,对于每个字符:
    - 如果当前字符已经出现过,且上次出现的位置在当前子串范围内,则更新start位置到上次出现位置的下一个位置。
    - 更新当前字符最后一次出现的位置。
    - 计算当前子串的长度,并更新最大长度。
3. 返回最大长度。

**代码分析:**
1. 初始化一个哈希表`charMap`来存储字符及其最后一次出现的位置。
2. 初始化`maxLength`和`start`变量,分别表示最长子串的长度和当前子串的起始位置。
3. 遍历字符串`s`,对于每个字符`c`:
    - 如果`charMap`中已经包含了`c`,且`charMap.get(c)`大于等于`start`,则更新`start`为`charMap.get(c) + 1`。这是因为如果当前字符在当前子串范围内出现过,则需要将子串的起始位置更新到上次出现位置的下一个位置。
    - 更新`charMap`中`c`的最后一次出现位置为`i`。
    - 计算当前子串的长度`i - start + 1`,并更新`maxLength`。
4. 最后返回`maxLength`。

## 代码

```java
public int lengthOfLongestSubstring(String s) {  
    // 用于存储字符及其最后一次出现的位置  
    Map<Character, Integer> charMap = new HashMap<>();  
    int maxLength = 0;  
    int start = 0;  
  
    for (int i = 0; i < s.length(); i++) {  
        char c = s.charAt(i);  
        // 如果当前字符已经出现过,且上次出现的位置在当前子串范围内,则更新start位置  
        if (charMap.containsKey(c) && charMap.get(c) >= start) {  
            start = charMap.get(c) + 1;  
        }  
        // 更新当前字符最后一次出现的位置  
        charMap.put(c, i);  
        // 计算当前子串的长度,并更新最大长度  
        maxLength = Math.max(maxLength, i - start + 1);  
    }  
  
    return maxLength;  
}
```

## 效率

- 时间复杂度: O(n),其中n是字符串s的长度。我们只需要遍历字符串一次。
- 空间复杂度: O(min(m, n)),其中m是字符集的大小。我们使用哈希表存储字符及其最后一次出现的位置,最坏情况下需要存储整个字符串,即空间复杂度为O(n)。但是,因为字符集通常很小(128个ASCII字符或256个扩展ASCII字符),所以在实际情况下,空间复杂度接近O(m)。

# 49. 丑数

## 题目

我们把只包含质因子2、3和5的数称作丑数(Ugly Number)。求按从小到大的顺序的第n个丑数。

示例:
输入: n=10
输出: 12
解释: 1,2,3,4,5,6,8,9,10,12 是前 10 个丑数。

限制:
1. 1 是丑数。
2. n 不超过1690。

## 思路

1. 创建一个长度为n的数组`uglyNumbers`来存储前n个丑数。  
2. 初始化第一个丑数为1。  
3. 使用三个索引`index2`、`index3`和`index5`来分别记录下一个丑数应该乘以2、3或5的位置。  
4. 从第二个丑数开始计算,每次选择当前三个索引对应的最小值作为下一个丑数,并更新对应的索引。  
5. 返回第n个丑数。  
  
**代码分析:**  
1. 初始化一个长度为n的数组`uglyNumbers`来存储前n个丑数,并将第一个丑数设置为1。  
2. 初始化三个索引`index2`、`index3`和`index5`,用于记录下一个丑数应该乘以2、3或5的位置。  
3. 从第二个丑数开始计算,每次选择当前三个索引对应的最小值作为下一个丑数,并将其存储在`uglyNumbers[i]`中。  
4. 更新对应的索引,使其指向下一个应该乘以2、3或5的数。  
5. 最后返回第n个丑数`uglyNumbers[n-1]`。  
  
## 代码

```java
public int nthUglyNumber(int n) {  
    // 用于存储前n个丑数  
    int[] uglyNumbers = new int[n];  
    // 初始化第一个丑数为1  
    uglyNumbers[0] = 1;  
  
    // 用于记录下一个丑数应该乘以2、3或5的索引  
    int index2 = 0, index3 = 0, index5 = 0;  
  
    // 从第二个丑数开始计算  
    for (int i = 1; i < n; i++) {  
        // 选择下一个丑数为当前三个索引对应的最小值  
        int nextUgly = Math.min(uglyNumbers[index2] * 2, Math.min(uglyNumbers[index3] * 3, uglyNumbers[index5] * 5));  
        uglyNumbers[i] = nextUgly;  
  
        // 更新对应的索引,使其指向下一个应该乘以2、3或5的数  
        if (nextUgly == uglyNumbers[index2] * 2) {  
            index2++;  
        }  
        if (nextUgly == uglyNumbers[index3] * 3) {  
            index3++;  
        }  
        if (nextUgly == uglyNumbers[index5] * 5) {  
            index5++;  
        }  
    }  
  
    return uglyNumbers[n - 1];  
}
```

## 效率

- 时间复杂度: O(n),我们需要计算前n个丑数,每次计算都需要O(1)的时间。  
- 空间复杂度: O(n),我们需要使用一个长度为n的数组来存储前n个丑数。  
- 这个解决方案的时间复杂度和空间复杂度都是线性的,是一个高效的解决方案。

# 50. 第一个只出现一次的字符

## 题目

在字符串s中找出第一个只出现一次的字符。如果没有, 返回一个单空格。s只包含小写字母。

示例 1:
输入: s = "abaccdeff"
输出: 'b'

示例2:
输入: s=""
输出: ''

限制: 0 <= s 的长度 <= 50000

## 思路

1. 创建一个长度为n的数组`uglyNumbers`来存储前n个丑数。  
2. 初始化第一个丑数为1。  
3. 使用三个索引`index2`、`index3`和`index5`来分别记录下一个丑数应该乘以2、3或5的位置。  
4. 从第二个丑数开始计算,每次选择当前三个索引对应的最小值作为下一个丑数,并更新对应的索引。  
5. 返回第n个丑数。  
  
**代码分析:**  
1. 初始化一个长度为n的数组`uglyNumbers`来存储前n个丑数,并将第一个丑数设置为1。  
2. 初始化三个索引`index2`、`index3`和`index5`,用于记录下一个丑数应该乘以2、3或5的位置。  
3. 从第二个丑数开始计算,每次选择当前三个索引对应的最小值作为下一个丑数,并将其存储在`uglyNumbers[i]`中。  
4. 更新对应的索引,使其指向下一个应该乘以2、3或5的数。  
5. 最后返回第n个丑数`uglyNumbers[n-1]`。  

## 代码

```java
public int nthUglyNumber(int n) {  
    // 用于存储前n个丑数  
    int[] uglyNumbers = new int[n];  
    // 初始化第一个丑数为1  
    uglyNumbers[0] = 1;  
  
    // 用于记录下一个丑数应该乘以2、3或5的索引  
    int index2 = 0, index3 = 0, index5 = 0;  
  
    // 从第二个丑数开始计算  
    for (int i = 1; i < n; i++) {  
        // 选择下一个丑数为当前三个索引对应的最小值  
        int nextUgly = Math.min(uglyNumbers[index2] * 2, Math.min(uglyNumbers[index3] * 3, uglyNumbers[index5] * 5));  
        uglyNumbers[i] = nextUgly;  
  
        // 更新对应的索引,使其指向下一个应该乘以2、3或5的数  
        if (nextUgly == uglyNumbers[index2] * 2) {  
            index2++;  
        }  
        if (nextUgly == uglyNumbers[index3] * 3) {  
            index3++;  
        }  
        if (nextUgly == uglyNumbers[index5] * 5) {  
            index5++;  
        }  
    }  
    return uglyNumbers[n - 1];  
}
```

## 效率

- 时间复杂度: O(n),我们需要计算前n个丑数,每次计算都需要O(1)的时间。  
- 空间复杂度: O(n),我们需要使用一个长度为n的数组来存储前n个丑数。  

# 51. 数组中的逆序对

## 题目

在数组中的两个数字, 如果前面一个数字大于后面的数字, 则这两个数字组成一个逆序对。输入一个数组, 求出这个数组中的逆序对的总数。

示例1:
输入: [7,5,6,4]
输出: 5

限制: 0 <= 数组长度 <= 50000

## 思路

1. 使用归并排序的思想,递归地将数组分成左右两部分,并计算每个部分的逆序对数量。  
2. 在合并左右两部分时,计算跨越中间的逆序对数量。  
3. 最终返回逆序对的总数。  
  
**代码分析:**  
1. `reversePairs`方法是入口函数,初始化逆序对的数量为0,并调用递归函数`mergeSort`。  
2. `mergeSort`方法递归地将数组分成左右两部分,并计算每个部分的逆序对数量。  
3. `merge`方法合并左右两部分,并计算跨越中间的逆序对数量。具体做法是:  
	- 创建一个临时数组`temp`来存储合并后的数组。  
	- 比较左右两部分的元素,如果左部分的元素大于右部分的元素,则说明存在逆序对,并更新逆序对的数量。  
	- 将较小的元素添加到临时数组中。  
	- 将剩余的元素添加到临时数组中。  
	- 将临时数组中的元素复制回原数组。  
1. 最后返回逆序对的总数。  

## 代码

```java
public int reversePairs(int[] nums) {  
    // 初始化逆序对的数量为0  
    int count = 0;  
    // 递归计算逆序对的数量  
    mergeSort(nums, 0, nums.length - 1, count);  
    return count;  
}  
  
private int mergeSort(int[] nums, int left, int right, int count) {  
    // 如果数组只有一个元素,直接返回  
    if (left >= right) {  
        return 0;  
    }  
    // 计算中间索引  
    int mid = left + (right - left) / 2;  
    // 递归计算左半部分的逆序对数量  
    count = mergeSort(nums, left, mid, count);  
    // 递归计算右半部分的逆序对数量  
    count = mergeSort(nums, mid + 1, right, count);  
    // 合并左右两部分,并计算跨越中间的逆序对数量  
    count = merge(nums, left, mid, right, count);  
  
    return count;  
}  
  
private int merge(int[] nums, int left, int mid, int right, int count) {  
    // 创建临时数组,用于存储合并后的数组  
    int[] temp = new int[right - left + 1];  
    int i = left, j = mid + 1, k = 0;  
    // 合并左右两部分,并计算跨越中间的逆序对数量  
    while (i <= mid && j <= right) {  
        if (nums[i] > nums[j]) {  
            count += right - j + 1;  
            temp[k++] = nums[i++];  
        } else {  
            temp[k++] = nums[j++];  
        }  
    }  
    // 将剩余元素添加到临时数组中  
    while (i <= mid) {  
        temp[k++] = nums[i++];  
    }  
    while (j <= right) {  
        temp[k++] = nums[j++];  
    }  
    // 将临时数组中的元素复制回原数组  
    for (int l = 0; l < temp.length; l++) {  
        nums[left + l] = temp[l];  
    }  
    return count;  
}
```

## 效率

- 时间复杂度: O(nlogn),其中n是数组的长度。我们使用归并排序的思想,需要将数组递归地分成左右两部分,每次合并时需要遍历左右两部分,因此时间复杂度为O(nlogn)。  
- 空间复杂度: O(n),我们需要使用一个临时数组来存储合并后的数组,因此空间复杂度为O(n)。  

# 52. 两个链表的第一个公共节点

## 题目

给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。

**示例 1：**
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'
解释：相交节点的值为 8 。 从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。

**示例 2：**
输入：intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Intersected at '2'
解释：相交节点的值为 2 。 从各自的表头开始算起，链表 A 为 [1,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。

**示例 3：**
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。

**提示:**
- 链表 A 和链表 B 的节点数量分别为 `m` 和 `n`
- 0 <= `m`, `n` <= 3 * 10^4
- 1 <= `skipA` <= `m`
- 1 <= `skipB` <= `n`
- 如果 `listA` 和 `listB` 没有交点,`intersectVal` 为 0
- 如果 `listA` 和 `listB` 有交点,`intersectVal == listA[skipA] == listB[skipB]`

## 思路

1. 如果两个链表都为空,则没有公共节点,返回 `null`。
2. 分别遍历两个链表,直到找到公共节点或者两个链表都遍历完。
3. 如果 `ptrA` 不为空,则移动到下一个节点,否则将其移动到 `headB`。
4. 如果 `ptrB` 不为空,则移动到下一个节点,否则将其移动到 `headA`。
5. 当 `ptrA` 和 `ptrB` 相等时,说明找到了公共节点,返回该节点。

**代码分析:**
1. 首先判断两个链表是否都为空,如果是,则没有公共节点,返回 `null`。
2. 定义两个指针 `ptrA` 和 `ptrB`,分别指向两个链表的头节点。
3. 在 `while` 循环中,如果 `ptrA` 不为空,则移动到下一个节点,否则将其移动到 `headB`。同理,如果 `ptrB` 不为空,则移动到下一个节点,否则将其移动到 `headA`。
4. 当 `ptrA` 和 `ptrB` 相等时,说明找到了公共节点,返回该节点。

## 代码

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {  
    // 如果两个链表都为空,则没有公共节点  
    if (headA == null || headB == null) {  
        return null;  
    }  
  
    // 分别遍历两个链表,直到找到公共节点或者两个链表都遍历完  
    ListNode ptrA = headA, ptrB = headB;  
    while (ptrA != ptrB) {  
        // 如果 ptrA 不为空,则移动到下一个节点,否则将其移动到 headB        
        ptrA = (ptrA != null) ? ptrA.next : headB;  
        // 如果 ptrB 不为空,则移动到下一个节点,否则将其移动到 headA        
        ptrB = (ptrB != null) ? ptrB.next : headA;  
    }  
  
    // 返回公共节点  
    return ptrA;  
}
```

## 效率

- 时间复杂度: O(m+n),其中 m 和 n 分别是两个链表的长度。我们需要遍历两个链表,直到找到公共节点或者两个链表都遍历完。
- 空间复杂度: O(1),我们只使用了两个指针,因此空间复杂度为常数级别。

# 53. 在排序数组中查找数字Ⅰ

## 题目

统计一个数字在排序数组中出现的次数。

示例1:
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2

示例2:
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0

提示:
- 0 <= nums.length <= 105
- -109 <= nums[i] <= 109
- nums 是一个非递减数组
- -109 <= target <= 109

## 思路

1. 使用二分查找找到目标值第一次出现的索引和最后一次出现的索引。
2. 如果目标值不存在,返回 `[-1, -1]`。
3. 否则返回目标值出现的次数。

**代码分析:**
1. 定义两个辅助方法 `findFirstIndex` 和 `findLastIndex`,分别用于查找目标值第一次和最后一次出现的索引。
2. 在 `findFirstIndex` 方法中,使用二分查找找到目标值第一次出现的索引。如果找到目标值,则向左搜索,尝试找到更小的索引。
3. 在 `findLastIndex` 方法中,使用二分查找找到目标值最后一次出现的索引。如果找到目标值,则向右搜索,尝试找到更大的索引。
4. 在 `searchRange` 方法中,调用 `findFirstIndex` 和 `findLastIndex` 方法,并根据结果返回目标值出现的次数。

## 代码

```java
public int[] searchRange(int[] nums, int target) {  
    // 使用二分查找找到目标值的第一次和最后一次出现的索引  
    int firstIndex = findFirstIndex(nums, target);  
    int lastIndex = findLastIndex(nums, target);  
  
    // 如果目标值不存在,返回 [-1, -1]    if (firstIndex == -1 || lastIndex == -1) {  
        return new int[]{-1, -1};  
    }  
  
    // 否则返回目标值出现的次数  
    return new int[]{firstIndex, lastIndex};  
}
private int findFirstIndex(int[] nums, int target) {  
    int left = 0, right = nums.length - 1;  
    int firstIndex = -1;  
  
    // 使用二分查找找到目标值第一次出现的索引  
    while (left <= right) {  
        int mid = left + (right - left) / 2;  
        if (nums[mid] == target) {  
            firstIndex = mid;  
            right = mid - 1; // 向左搜索,尝试找到更小的索引  
        } else if (nums[mid] < target) {  
            left = mid + 1;  
        } else {  
            right = mid - 1;  
        }  
    }  
  
    return firstIndex;  
}  
private int findLastIndex(int[] nums, int target) {  
    int left = 0, right = nums.length - 1;  
    int lastIndex = -1;  
  
    // 使用二分查找找到目标值最后一次出现的索引  
    while (left <= right) {  
        int mid = left + (right - left) / 2;  
        if (nums[mid] == target) {  
            lastIndex = mid;  
            left = mid + 1; // 向右搜索,尝试找到更大的索引  
        } else if (nums[mid] < target) {  
            left = mid + 1;  
        } else {  
            right = mid - 1;  
        }  
    }  
  
    return lastIndex;  
}
```

## 效率

- 时间复杂度: O(log n),其中 n 是数组的长度。我们使用二分查找来找到目标值第一次和最后一次出现的索引,每次查找的时间复杂度为 O(log n)。
- 空间复杂度: O(1),我们只使用了几个变量来存储中间结果,因此空间复杂度为常数级别。

# 54. 0 ~ n-1 中缺失的数字Ⅱ

## 题目

一个长度为n-1的递增排序数组中的所有数字都是唯一的, 并且每个数字都在范围0~n-1之内。在范围0~n-1内的n个数字中有且只有一个数字不在该数组中, 请找出这个数字。

示例1:
输入: [0,1,3]
输出: 2

示例2:
输入: [0,1,2,3,4,5,6,7,9]
输出: 8

限制: 1 <= 数组长度 <= 10000

## 思路

1. 使用异或运算来找到缺失的数字。
2. 首先计算 0 到 n-1 的异或值,其中 n 是数组长度加 1。
3. 然后计算数组元素的异或值。
4. 最后,缺失的数字就是这两个异或值的结果。

**代码分析:**

1. 在 `missingNumber` 方法中,我们首先计算 0 到 n-1 的异或值,其中 n 是数组长度加 1。
2. 然后计算数组元素的异或值。
3. 最后,我们返回这两个异或值的结果,就是缺失的数字。

## 代码

```java
public int missingNumber(int[] nums) {  
    // 使用异或运算找到缺失的数字  
    int n = nums.length + 1;  
    int xor1 = 0;  
    int xor2 = 0;  
  
    // 计算 0 到 n-1 的异或值  
    for (int i = 0; i < n; i++) {  
        xor1 ^= i;  
    }  
  
    // 计算数组元素的异或值  
    for (int num : nums) {  
        xor2 ^= num;  
    }  
  
    // 缺失的数字就是两个异或值的结果  
    return xor1 ^ xor2;  
}
```

## 效率

- 时间复杂度: O(n),其中 n 是数组的长度。我们只需要遍历数组一次,并进行几次异或运算。
- 空间复杂度: O(1),我们只使用了几个变量来存储中间结果,因此空间复杂度为常数级别。

# 55. 二叉搜索树的第k大节点

## 题目

给定一棵二叉搜索树,请找出其中第 k 大的节点。

示例 1:
输入: root = [3,1,4,null,2], k = 1
输出: 4

示例 2:
输入: root = [5,3,6,2,4,null,null,1], k = 3
输出: 4

提示:
- 二叉搜索树的根节点为 root
- 0 < k ≤ 二叉搜索树元素个数

## 思路

1. 由于二叉搜索树的中序遍历(右-根-左)是一个递增序列,因此我们可以利用这个特性来找到第 k 大的节点。
2. 我们使用一个计数器 `count` 来记录遍历的节点数,当 `count` 等于 `k` 时,我们就找到了第 k 大的节点,并更新结果 `result`。

**代码分析:**
1. 在 `kthLargest` 方法中,我们调用 `inorderTraversal` 方法来进行中序遍历。
2. 在 `inorderTraversal` 方法中,我们先遍历右子树,然后更新计数器 `count`,如果 `count` 等于 `k`,则更新结果 `result`。最后,我们遍历左子树。
3. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
private int count = 0;
private int result = 0;

public int kthLargest(TreeNode root, int k) {
	// 使用中序遍历(右-根-左)来找到第 k 大的节点
	inorderTraversal(root, k);
	return result;
}

private void inorderTraversal(TreeNode node, int k) {
	if (node == null) {
		return;
	}
	// 先遍历右子树
	inorderTraversal(node.right, k);
	// 统计遍历的节点数,如果是第 k 个节点,则更新结果
	count++;
	if (count == k) {
		result = node.val;
		return;
	}
	// 再遍历左子树
	inorderTraversal(node.left, k);
}
```

## 效率

- 时间复杂度: O(n),其中 n 是二叉搜索树的节点数。我们需要遍历整个二叉搜索树,时间复杂度为 O(n)。
- 空间复杂度: O(h),其中 h 是二叉搜索树的高度。在递归调用过程中,最多需要存储 h 个函数调用栈帧,因此空间复杂度为 O(h)。在最坏情况下,二叉搜索树退化为链表,h 为 n,空间复杂度为 O(n)。

# 56. 二叉树的深度

## 题目

给定一个二叉树,找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例:  
给定二叉树 [3,9,20,null,null,15,7],

`3`
/  
9 20  
/  
15 7

返回它的最大深度 3 。

## 思路

1. 如果根节点为空,则返回 0,表示树的深度为 0。
2. 递归计算左子树和右子树的最大深度,并返回最大值加 1,即为整棵树的最大深度。

**代码分析:**

1. 在 `maxDepth` 方法中,我们首先判断根节点是否为空。如果为空,则返回 0。
2. 然后,我们递归计算左子树和右子树的最大深度,并返回最大值加 1。
3. 在 `main` 方法中,我们构建了一个测试用例,并验证了解决方案的正确性。

## 代码

```java 
public int maxDepth(TreeNode root) {         
	// 如果根节点为空,则返回 0         
	if (root == null) { return 0; }                 
	// 递归计算左子树和右子树的最大深度,并返回最大值加 1         
	int leftDepth = maxDepth(root.left);         
	int rightDepth = maxDepth(root.right);         
	return Math.max(leftDepth, rightDepth) + 1;     
}
```

## 效率

- 时间复杂度: O(n),其中 n 是二叉树的节点数。我们需要遍历整个二叉树,时间复杂度为 O(n)。
- 空间复杂度: O(h),其中 h 是二叉树的高度。在递归调用过程中,最多需要存储 h 个函数调用栈帧,因此空间复杂度为 O(h)。在最坏情况下,二叉树退化为链表,h 为 n,空间复杂度为 O(n)。

# 57. 平衡二叉树

## 题目

给定一个二叉树,判断它是否是高度平衡的二叉树。

本题中,一棵高度平衡二叉树的定义是: 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

示例 1:
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7

返回 true 。

示例 2:
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4

返回 false 。


## 思路

1. 如果根节点为空,则返回 true,表示这棵树是平衡的。
2. 递归计算左子树和右子树的高度,如果高度差大于 1,则返回 false,表示这棵树不是平衡的。
3. 递归检查左子树和右子树是否平衡,如果都平衡,则返回 true,表示这棵树是平衡的。

**代码分析:**
1. 在 `isBalanced` 方法中,我们首先判断根节点是否为空。如果为空,则返回 true。
2. 然后,我们递归计算左子树和右子树的高度,并检查高度差是否大于 1。如果大于 1,则返回 false。
3. 最后,我们递归检查左子树和右子树是否平衡,如果都平衡,则返回 true。
4. 在 `getHeight` 方法中,我们递归计算节点的高度,如果节点为空,则返回 0。
5. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public boolean isBalanced(TreeNode root) {
	// 如果根节点为空,则返回 true
	if (root == null) {
		return true;
	}
	
	// 递归计算左子树和右子树的高度,如果高度差大于 1,则返回 false
	int leftHeight = getHeight(root.left);
	int rightHeight = getHeight(root.right);
	if (Math.abs(leftHeight - rightHeight) > 1) {
		return false;
	}
	
	// 递归检查左子树和右子树是否平衡
	return isBalanced(root.left) && isBalanced(root.right);
}

private int getHeight(TreeNode node) {
	// 如果节点为空,则返回 0
	if (node == null) {
		return 0;
	}
	
	// 递归计算左子树和右子树的高度,并返回最大值加 1
	int leftHeight = getHeight(node.left);
	int rightHeight = getHeight(node.right);
	return Math.max(leftHeight, rightHeight) + 1;
}
```

## 效率

- 时间复杂度: O(n),其中 n 是二叉树的节点数。我们需要遍历整个二叉树,计算每个节点的高度,时间复杂度为 O(n)。
- 空间复杂度: O(h),其中 h 是二叉树的高度。在递归调用过程中,最多需要存储 h 个函数调用栈帧,因此空间复杂度为 O(h)。在最坏情况下,二叉树退化为链表,h 为 n,空间复杂度为 O(n)。

# 58. 数组中数字出现的次数 Ⅰ

## 题目

一个整型数组 nums 里除两个数字之外,其他数字都出现了两次。请写程序我出这两个只出现一次的数字。要求时间复杂度是O(n), 空间复杂度是O(1)

示例1:
输入: nums = [4,1,4,6]
输出: [1,6] 或 [6,1]

示例2:
输入: nums = [1,2,10,4,1,4,3,3]
输出: [2,10] 或 [10,2]

限制: 2 <= nums.length <= 10000

## 思路

1. 首先,我们使用异或运算找出两个只出现一次的数字的异或值。由于其他数字都出现了两次,在异或运算中会被抵消掉,最终剩下的就是两个只出现一次的数字的异或值。
2. 接下来,我们找出异或值中最低位的 1,作为区分两个数字的依据。
3. 最后,我们根据最低位的 1 将数组分成两组,两个只出现一次的数字会被分到不同的组。我们再次使用异或运算,分别找出两个组中只出现一次的数字。

**代码分析:**
1. 在 `singleNumber` 方法中,我们首先使用异或运算找出两个只出现一次的数字的异或值。
2. 然后,我们找出异或值中最低位的 1,作为区分两个数字的依据。
3. 最后,我们根据最低位的 1 将数组分成两组,两个只出现一次的数字会被分到不同的组。我们再次使用异或运算,分别找出两个组中只出现一次的数字。
4. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public int[] singleNumber(int[] nums) {  
    // 1. 使用异或运算找出两个只出现一次的数字的异或值  
    int xor = 0;  
    for (int num : nums) {  
        xor ^= num;  
    }  
  
    // 2. 找出异或值中最低位的 1,作为区分两个数字的依据  
    int mask = xor & (-xor);  
  
    // 3. 根据最低位的 1 将数组分成两组,两个只出现一次的数字会被分到不同的组  
    int num1 = 0, num2 = 0;  
    for (int num : nums) {  
        if ((num & mask) == 0) {  
            num1 ^= num;  
        } else {  
            num2 ^= num;  
        }  
    }  
  
    return new int[]{num1, num2};  
}
```

## 效率

- 时间复杂度: O(n),其中 n 是数组的长度。我们需要遍历整个数组一次,时间复杂度为 O(n)。
- 空间复杂度: O(1),我们只使用了常量级的额外空间,因此空间复杂度为 O(1)。

# 59. 数组中数字出现的次数 Ⅱ

## 题目

在一个数组 nums 中除一个数字只出现一次之外, 其他数字都出现了三次。请找出那个只出现一次的数字。

示例1:
输入: nums = [3,4,3,3]
输出: 4

示例2:
输入: nums = [9,1,7,9,7,9,7]
输出: 1

限制:
- 1 <= nums. length <= 10000
- 1 <= nums[i] < 2^31

## 思路

1. 我们使用一个长度为 32 的数组 `bits` 来记录每一位上 1 的出现次数。
2. 遍历数组 `nums` 中的每个数字,并更新 `bits` 数组中相应位置的计数。
3. 最后,我们根据 `bits` 数组中每一位上 1 的出现次数,找出只出现一次的数字。由于其他数字都出现了三次,在每一位上 1 的出现次数都是 3 的倍数,因此我们只需要找出那些出现次数不是 3 的倍数的位置,并将它们组合成最终的结果。

**代码分析:**
1. 在 `singleNumber` 方法中,我们首先初始化一个长度为 32 的数组 `bits` 来记录每一位上 1 的出现次数。
2. 然后,我们遍历数组 `nums` 中的每个数字,并更新 `bits` 数组中相应位置的计数。
3. 最后,我们根据 `bits` 数组中每一位上 1 的出现次数,找出只出现一次的数字。我们只需要将那些出现次数不是 3 的倍数的位置组合成最终的结果。
4. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public int singleNumber(int[] nums) {  
    // 1. 使用位运算计算每一位上 1 的出现次数  
    int[] bits = new int[32];  
    for (int num : nums) {  
        for (int i = 0; i < 32; i++) {  
            if ((num & (1 << i)) != 0) {  
                bits[i] += 1;  
            }  
        }  
    }  
  
    // 2. 根据每一位上 1 的出现次数,找出只出现一次的数字  
    int result = 0;  
    for (int i = 0; i < 32; i++) {  
        if (bits[i] % 3 != 0) {  
            result |= (1 << i);  
        }  
    }  
    return result;  
}
```

## 效率

- 时间复杂度: O(n),其中 n 是数组的长度。我们需要遍历整个数组一次,时间复杂度为 O(n)。
- 空间复杂度: O(1),我们只使用了长度为 32 的额外数组,因此空间复杂度为 O(1)。

# 60. 和为s的两个数字

## 题目

这个问题是 LeetCode 上的一个题目,称为"和为 s 的两个数字"。

题目描述:
给定一个递增排序的整型数组 `nums` 和一个目标值 `target`。在数组中找到两个数字,使它们的和等于 `target`。如果存在多对数字的和等于 `target`，则输出任意一对即可。

示例 1:
输入: nums = [1,2,3,4,5,6,7,8,9], target = 9
输出: [2,7]
解释: 2 + 7 = 9

示例 2:
输入: nums = [1,2,4,6,10], target = 10
输出: [4,6]
解释: 4 + 6 = 10

限制:
- 1 <= nums.length <= 10^5
- 1 <= nums[i] <= 10^6
- 1 <= target <= 10^6


## 思路

1. 我们使用两个指针 `left` 和 `right`，分别指向数组的头部和尾部。
2. 我们移动这两个指针,直到找到和为 `target` 的两个数字。如果当前两个数字的和小于 `target`，我们将 `left` 指针向右移动;如果当前两个数字的和大于 `target`，我们将 `right` 指针向左移动。
3. 如果找到了和为 `target` 的两个数字,我们返回它们。如果没有找到,我们返回一个空数组。

**代码分析:**
1. 在 `twoSum` 方法中,我们首先初始化两个指针 `left` 和 `right`。
2. 然后,我们使用一个 `while` 循环来移动这两个指针,直到找到和为 `target` 的两个数字。
3. 在循环中,我们计算当前两个数字的和,并根据与 `target` 的比较结果来移动指针。
4. 如果找到了和为 `target` 的两个数字,我们返回它们。如果没有找到,我们返回一个空数组。
5. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public int[] twoSum(int[] nums, int target) {
	// 1. 使用双指针,一个指向数组头部,一个指向数组尾部
	int left = 0, right = nums.length - 1;
	
	// 2. 移动指针,直到找到和为 target 的两个数字
	while (left < right) {
		int sum = nums[left] + nums[right];
		if (sum == target) {
			return new int[]{nums[left], nums[right]};
		} else if (sum < target) {
			left++;
		} else {
			right--;
		}
	}
	
	// 3. 如果没有找到,返回一个空数组
	return new int[0];
}
```

## 效率

- 时间复杂度: O(n),其中 n 是数组的长度。我们只需要遍历数组一次,时间复杂度为 O(n)。
- 空间复杂度: O(1),我们只使用了常量级的额外空间,因此空间复杂度为 O(1)。

# 61. 和为s的连续正数序列

## 题目

输入一个正整数 `target`，输出所有和为 `target` 的连续正数序列（至少含有两个数）。

序列内按照从小到大的顺序排列，序列间按照首个数字从小到大的顺序排列。

示例 1:
输入: target = 9
输出: \[[2,3,4],[4,5]]
解释: 和为 9 的连续正数序列有 `[2,3,4]` 和 `[4,5]` 两种。

示例 2:
输入: target = 15
输出: \[[1,2,3,4,5],[4,5,6],[7,8]]

限制:
- 1 <= target <= 10^5

## 思路

1. 我们使用两个指针 `left` 和 `right`，分别指向序列的起点和终点。
2. 我们初始化 `left` 为 1, `right` 为 2, `sum` 为 3。
3. 我们使用一个 `while` 循环来移动这两个指针,直到找到所有和为 `target` 的连续正数序列。
4. 在循环中,我们根据当前序列的和与 `target` 的比较结果来移动指针:
   - 如果当前序列的和等于 `target`，我们将当前序列添加到结果中,并将左指针向右移动,更新序列和。
   - 如果当前序列的和小于 `target`，我们将右指针向右移动,更新序列和。
   - 如果当前序列的和大于 `target`，我们将左指针向右移动,更新序列和。
5. 最后,我们将结果转换为数组并返回。

**代码分析:**
1. 在 `findContinuousSequence` 方法中,我们首先初始化两个指针 `left` 和 `right`,以及序列的初始和 `sum`。
2. 然后,我们使用一个 `while` 循环来移动这两个指针,直到找到所有和为 `target` 的连续正数序列。
3. 在循环中,我们根据当前序列的和与 `target` 的比较结果来移动指针,并将找到的序列添加到结果中。
4. 最后,我们将结果转换为数组并返回。
5. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public int[][] findContinuousSequence(int target) {
	// 1. 使用双指针,一个指向序列的起点,一个指向序列的终点
	int left = 1, right = 2;
	int sum = 3; // 初始化序列的和为 3
	
	// 2. 使用 List 存储结果
	List<int[]> result = new ArrayList<>();
	
	// 3. 移动指针,直到找到所有和为 target 的连续正数序列
	while (left < right) {
		if (sum == target) {
			// 找到一个序列,将其添加到结果中
			int[] sequence = new int[right - left + 1];
			for (int i = left; i <= right; i++) {
				sequence[i - left] = i;
			}
			result.add(sequence);
			
			// 将左指针向右移动,更新序列和
			sum -= left;
			left++;
		} else if (sum < target) {
			// 将右指针向右移动,更新序列和
			right++;
			sum += right;
		} else {
			// 将左指针向右移动,更新序列和
			sum -= left;
			left++;
		}
	}
	// 4. 将结果转换为数组并返回
	return result.toArray(new int[result.size()][]);
}
```

## 效率

- 时间复杂度: O(sqrt(target)),其中 `target` 是给定的目标值。我们需要遍历从 1 到 `sqrt(target)` 之间的所有可能的序列起点,因此时间复杂度为 O(sqrt(target))。
- 空间复杂度: O(1),我们只使用了常量级的额外空间,因此空间复杂度为 O(1)。

# 62. 翻转单词顺序

## 题目

给定一个字符串,逆序输出字符串中的单词。单词是由非空格字符组成的字符序列。输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。

示例 1:
输入: "the sky is blue"
输出: "blue is sky the"

示例 2:
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。

示例 3:
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格,将反转后单词间的空格减少到只含一个。

说明:
- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。
- 如果两个单词间有多余的空格,将反转后单词间的空格减少到只含一个。

## 思路

1. 首先,我们去除字符串两端的空格。
2. 然后,我们将字符串分割为单词数组。这里使用正则表达式 `"\\s+"` 来分割字符串,它可以匹配一个或多个空白字符。
3. 接下来,我们反转单词数组。使用双指针 `left` 和 `right` 交换数组中对应位置的单词。
4. 最后,我们将反转后的单词数组拼接成字符串并返回。

**代码分析:**
1. 在 `reverseWords` 方法中,我们首先去除字符串两端的空格,使用 `trim()` 方法。
2. 然后,我们使用 `split()` 方法将字符串分割为单词数组,分割规则是一个或多个空白字符。
3. 接下来,我们使用双指针 `left` 和 `right` 交换数组中对应位置的单词,实现单词数组的反转。
4. 最后,我们使用 `StringBuilder` 拼接反转后的单词数组,并返回结果字符串。
5. 在 `main` 方法中,我们构建了三个测试用例,并验证了解决方案的正确性。

## 代码

```java
public String reverseWords(String s) {
	// 1. 去除字符串两端的空格
	s = s.trim();
	
	// 2. 将字符串分割为单词数组
	String[] words = s.split("\\s+");
	
	// 3. 反转单词数组
	int left = 0, right = words.length - 1;
	while (left < right) {
		String temp = words[left];
		words[left] = words[right];
		words[right] = temp;
		left++;
		right--;
	}
	
	// 4. 拼接反转后的单词数组
	StringBuilder sb = new StringBuilder();
	for (int i = 0; i < words.length; i++) {
		sb.append(words[i]);
		if (i < words.length - 1) {
			sb.append(" ");
		}
	}
	
	return sb.toString();
}
```

## 效率

- 时间复杂度: O(n),其中 n 是输入字符串的长度。我们需要遍历字符串两次,一次是去除两端空格,一次是拼接反转后的单词数组。
- 空间复杂度: O(n),我们需要创建一个单词数组来存储分割后的单词,数组长度最大为 n。

# 63. 左旋转字符串

## 题目

给定一个字符串,逆序输出字符串中的单词。单词是由非空格字符组成的字符序列。输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。

示例 1:  
输入: "the sky is blue"  
输出: "blue is sky the"

示例 2:  
输入: " hello world! "  
输出: "world! hello"  
解释: 输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。

示例 3:  
输入: "a good example"  
输出: "example good a"  
解释: 如果两个单词间有多余的空格,将反转后单词间的空格减少到只含一个。

说明:
- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格,但是反转后的字符串中不能包括。
- 如果两个单词间有多余的空格,将反转后单词间的空格减少到只含一个。

## 思路

1. 首先,我们去除字符串两端的空格。
2. 然后,我们将字符串分割为单词数组。这里使用正则表达式 `"\\s+"` 来分割字符串,它可以匹配一个或多个空白字符。
3. 接下来,我们反转单词数组。使用双指针 `left` 和 `right` 交换数组中对应位置的单词。
4. 最后,我们将反转后的单词数组拼接成字符串并返回。

**代码分析:**
1. 在 `reverseWords` 方法中,我们首先去除字符串两端的空格,使用 `trim()` 方法。
2. 然后,我们使用 `split()` 方法将字符串分割为单词数组,分割规则是一个或多个空白字符。
3. 接下来,我们使用双指针 `left` 和 `right` 交换数组中对应位置的单词,实现单词数组的反转。
4. 最后,我们使用 `StringBuilder` 拼接反转后的单词数组,并返回结果字符串。
5. 在 `main` 方法中,我们构建了三个测试用例,并验证了解决方案的正确性。

## 代码

```java
public String reverseLeftWords(String s, int n) {  
    // 1. 将字符串转换为字符数组  
    char[] chars = s.toCharArray();  
  
    // 2. 反转整个字符数组  
    reverse(chars, 0, chars.length - 1);  
  
    // 3. 反转前 n 个字符  
    reverse(chars, 0, n - 1);  
  
    // 4. 反转剩余的字符  
    reverse(chars, n, chars.length - 1);  
  
    // 5. 将字符数组转换为字符串并返回  
    return new String(chars);  
}  
  
private void reverse(char[] chars, int start, int end) {  
    while (start < end) {  
        char temp = chars[start];  
        chars[start] = chars[end];  
        chars[end] = temp;  
        start++;  
        end--;  
    }  
}
```

## 效率

- 时间复杂度: O(n),其中 n 是输入字符串的长度。我们需要遍历字符串两次,一次是去除两端空格,一次是拼接反转后的单词数组。
- 空间复杂度: O(n),我们需要创建一个单词数组来存储分割后的单词,数组长度最大为 n。

# 64. 滑动窗口的最大值

## 题目

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

请你找出所有滑动窗口里的最大值。

示例 1:  
输入: nums = [1,3,-1,-3,5,3,6,7], k = 3
输出: [3,3,5,5,6,7]
解释:  
滑动窗口的位置 最大值

[1 3 -1] -3 5 3 6 7 3  
1 [3 -1 -3] 5 3 6 7 3  
1 3 [-1 -3 5] 3 6 7 5  
1 3 -1 [-3 5 3] 6 7 5  
1 3 -1 -3 [5 3 6] 7 6  
1 3 -1 -3 5 [3 6 7] 7

示例 2:  
输入: nums = [1], k = 1
输出: [1]

提示:
- 1 <= nums.length <= 10^5
- -10^4 <= nums[i] <= 10^4
- 1 <= k <= nums.length

## 思路

1. 我们使用一个双端队列 `deque` 来存储当前滑动窗口中的最大值的下标。
2. 我们遍历输入数组 `nums`。
    - 对于每个元素,我们从队列尾部移除所有小于当前元素的元素。这样可以保证队列中始终存储着当前滑动窗口中的最大值的下标。
    - 我们将当前元素的下标添加到队列尾部。
    - 如果队列头部元素已经不在当前滑动窗口内,我们将其从队列中移除。
    - 如果当前位置已经形成了大小为 `k` 的窗口,我们将队列头部元素(即当前滑动窗口的最大值)添加到结果数组中。
3. 最后,我们返回结果数组。

**代码分析:**
1. 在 `maxSlidingWindow` 方法中,我们首先初始化结果数组 `result`。
2. 然后,我们创建一个双端队列 `deque` 来存储当前滑动窗口中的最大值的下标。
3. 接下来,我们遍历输入数组 `nums`。
    - 在每次迭代中,我们从队列尾部移除所有小于当前元素的元素。这样可以保证队列中始终存储着当前滑动窗口中的最大值的下标。
    - 我们将当前元素的下标添加到队列尾部。
    - 如果队列头部元素已经不在当前滑动窗口内,我们将其从队列中移除。
    - 如果当前位置已经形成了大小为 `k` 的窗口,我们将队列头部元素(即当前滑动窗口的最大值)添加到结果数组中。
4. 最后,我们返回结果数组。
5. 在 `main` 方法中,我们构建了两个测试用例,并验证了解决方案的正确性。

## 代码

```java
public int[] maxSlidingWindow(int[] nums, int k) {  
    // 1. 初始化结果数组  
    int n = nums.length;  
    int[] result = new int[n - k + 1];  
  
    // 2. 创建双端队列  
    Deque<Integer> deque = new LinkedList<>();  
  
    // 3. 遍历数组  
    for (int i = 0; i < n; i++) {  
        // 3.1 从队列尾部移除小于当前元素的元素  
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {  
            deque.pollLast();  
        }  
  
        // 3.2 将当前元素下标添加到队列尾部  
        deque.offerLast(i);  
  
        // 3.3 如果队列头部元素已经不在窗口内,则移除队列头部元素  
        if (deque.peekFirst() == i - k) {  
            deque.pollFirst();  
        }  
  
        // 3.4 如果当前位置已经形成了大小为 k 的窗口,将队列头部元素添加到结果数组  
        if (i >= k - 1) {  
            result[i - k + 1] = nums[deque.peekFirst()];  
        }  
    }  
  
    return result;  
}
```

## 效率

- 时间复杂度: O(n),其中 n 是输入数组 `nums` 的长度。我们需要遍历数组一次,并在每次迭代中对双端队列进行操作。
- 空间复杂度: O(k),其中 k 是滑动窗口的大小。我们需要创建一个大小为 k 的双端队列来存储当前滑动窗口中的最大值的下标。

# 65. n个骰子的点数

## 题目

把n个骰子扔在地上,所有骰子朝上一面的点数之和为s。输入n, 打印出s的所有可能的值出现的概率。你需要用一个浮点数数组返回答案, 其中第i个元素代表这n个骰子所能掷出的点数集合中第i小的那个的概率。

示例1:
输入: 1
输出:
[0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]

示例2:
输入: 2
输出:
[0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13]

## 思路



## 代码



## 效率

# 66. 扑克牌中的顺子

## 题目

从若干副扑克牌中随机抽 5 张牌,判断是不是一个顺子, 即这5张牌是不是连续的。2~10为数字本身, A为1, J为11, Q为12, K为13, 而大、小王为0, 可以看成任意数字。A不能视为14。

示例1:
输入: [1,2,3,4,5]
输出: True

示例2:
输入: [0,0,1,2,5]
输出: True

限制:
- 数组长度为5
- 数组的数取值为[0,13]

## 思路

1. 首先,我们统计数组中大小王的数量,即值为 0 的元素个数。
2. 然后,我们对数组进行排序。
3. 接下来,我们遍历排序后的数组,检查是否存在对子(相同的牌)。如果存在对子,则不是顺子。
4. 对于每两个相邻的牌,我们计算它们之间的间隔。如果间隔大于大小王的数量,则不是顺子。
5. 如果遍历完数组后,都没有发现对子和间隔过大的情况,则说明这 5 张牌是一个顺子。

**代码分析**:
1. 在 `isStraight` 方法中,我们首先统计数组中大小王的数量。
2. 然后,我们对数组进行排序。
3. 接下来,我们遍历排序后的数组,从第一个非大小王的牌开始检查:
    - 如果遇到相同的牌,则说明存在对子,返回 `false`。
    - 否则,计算当前牌与下一张牌之间的间隔,如果间隔大于大小王的数量,则返回 `false`。
    - 如果间隔小于等于大小王的数量,则用大小王来填补这个间隔。
4. 如果遍历完数组后,都没有发现对子和间隔过大的情况,则说明这 5 张牌是一个顺子,返回 `true`。

## 代码

```java
public boolean isStraight(int[] nums) {  
    // 1. 统计大小王的数量  
    int jokers = 0;  
    for (int num : nums) {  
        if (num == 0) {  
            jokers++;  
        }  
    }  
  
    // 2. 对数组进行排序  
    Arrays.sort(nums);  
  
    // 3. 检查是否为顺子  
    for (int i = jokers; i < 4; i++) {  
        if (nums[i] == nums[i + 1]) {  
            // 如果有对子,则不是顺子  
            return false;  
        }  
        // 计算当前牌与下一张牌之间的间隔  
        int gap = nums[i + 1] - nums[i] - 1;  
        if (gap > jokers) {  
            // 如果间隔大于大小王的数量,则不是顺子  
            return false;  
        }  
        jokers -= gap;  
    }  
  
    return true;  
}
```

## 效率

- 时间复杂度: O(n log n)。主要是排序操作的时间复杂度。
- 空间复杂度: O(1)。我们只使用了常量额外空间。

# 67. 圆圈中最后剩下的数字

## 题目

0,1,...,n-1这n个数字排成一个圆圈, 从数字0开始,每次从这个圆圈里删除第m个数字(删除后从下一个数字开始计数)。求出这个圆圈里剩下的最后一个数字。

例如,0、1、2、3、4这5个数字组成一个圆圈, 从数字0开始每次删除第3个数字, 则删除的前4个数字依次是2、0、4、1, 因此最后剩下的数字是3.

示例1:
输入: n = 5, m = 3
输出: 3

示例2:
输入: n = 10, m = 17
输出: 2

限制:
- 1 <= n <= 10^5
- 1 <= m <= 10^6

## 思路

1. 我们可以使用数学推导的方式来解决这个问题。
2. 假设当前圆圈中剩余的元素索引为 `index`。
3. 当我们删除第 `m` 个元素时,下一个元素的索引应该是 `(index + m) % i`。这里 `i` 表示当前圆圈中剩余的元素个数。
4. 我们从索引 `0` 开始,逐步计算出最后剩下的元素的索引。

**代码分析**:
1. 在 `lastRemaining` 方法中,我们初始化了剩余元素的索引 `index` 为 `0`。
2. 然后,我们从 `2` 开始遍历 `n` 个元素。在每次迭代中,我们计算当前元素的索引,并更新 `index`。
3. 计算当前元素索引的公式为 `(index + m - 1) % i`。其中 `i` 表示当前圆圈中剩余的元素个数。
4. 最后,我们返回最终的 `index` 值,即为最后剩下的元素的索引。

## 代码

```java
public int lastRemaining(int n, int m) {  
    // 1. 初始化剩余元素的索引  
    int index = 0;  
  
    // 2. 从 0 开始遍历 n 个元素  
    for (int i = 2; i <= n; i++) {  
        // 3. 计算当前元素的索引  
        index = (index + m - 1) % i;  
    }  
  
    return index;  
}
```

## 效率

- 时间复杂度: O(n)。我们需要遍历 `n` 个元素,每次计算索引的复杂度为 O(1)。
- 空间复杂度: O(1)。我们只使用了常量额外空间。

# 68. 股票的最大利润

## 题目

假设把某股票的价格按照时间先后顺序存储在数组中, 请问买卖该股票一次可能获得的最大利润是多少?

示例1:
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2天(股票价格=1)的时候买入, 在第5天(股票价格=6)的时候卖出, 最大利润=6-1=5。注意利润不能是 7-1=6, 因为卖出价格需要大于买入价格。

示例2:
输入:[7,6,4,3,1]
输出:0
解释:在这种情况下, 没有交易完成, 所以最大利润为 0。

限制: 0 <= 数组长度 <= 10^5

## 思路

1. 我们可以采用贪心算法来解决这个问题。
2. 我们遍历数组,找到最小的买入价格和最大的卖出价格。
3. 如果当前价格大于最小买入价格,则计算利润并更新最大利润。
4. 否则,更新最小买入价格。

**代码分析**:
1. 在 `maxProfit` 方法中,我们初始化最大利润为 `0`。
2. 我们将第一个元素作为初始的最小买入价格。
3. 然后,我们从第二个元素开始遍历数组:
    - 如果当前价格大于最小买入价格,则计算利润并更新最大利润。
    - 否则,更新最小买入价格。
4. 最后,我们返回最大利润。

## 代码

```java
public int maxProfit(int[] prices) {  
    // 1. 初始化最大利润为 0    int maxProfit = 0;  
  
    // 2. 遍历数组,找到最小买入价格和最大卖出价格  
    int minPrice = prices[0];  
    for (int i = 1; i < prices.length; i++) {  
        // 3. 如果当前价格大于最小买入价格,则计算利润并更新最大利润  
        if (prices[i] > minPrice) {  
            maxProfit += prices[i] - minPrice;  
            minPrice = prices[i];  
        } else {  
            // 4. 否则,更新最小买入价格  
            minPrice = prices[i];  
        }  
    }  
  
    return maxProfit;  
}
```

## 效率

- 时间复杂度: O(n)。我们只需要遍历一次数组。
- 空间复杂度: O(1)。我们只使用了常量额外空间。

# 69. 求1+2+n

## 题目

求 1+2+ ... +n,要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句(A?B:C)。

示例1:
输入: n = 3
输出: 6

示例2:
输入: n = 9
输出: 45

限制: 1 <= n <= 10000

## 思路

1. 由于题目要求不能使用循环和条件判断语句,我们可以采用递归的方式来解决这个问题。
2. 递归的终止条件是 `n == 0`,此时返回 `0`。
3. 对于 `n > 0` 的情况,我们可以使用递归调用 `sumNums(n - 1)` 来计算 `1 + 2 + ... + (n-1)`,然后将当前的 `n` 加上即可。

**代码分析**:

1. 在 `sumNums` 方法中,我们使用递归的方式来计算 `1 + 2 + ... + n`。
2. 递归的终止条件是 `n == 0`,此时返回 `0`。
3. 对于 `n > 0` 的情况,我们使用 `n + sumNums(n - 1)` 来计算结果。这里使用了三元运算符 `?:` 来代替条件判断语句。

## 代码

```java
public int sumNums(int n) {
	// 1. 使用递归的方式计算 1 + 2 + ... + n
	return n > 0 ? n + sumNums(n - 1) : 0;
}
```

## 效率

- 时间复杂度: O(n)。我们需要递归 `n` 次才能得到最终结果。
- 空间复杂度: O(n)。由于递归调用,会在栈上产生 `n` 个栈帧。

# 70. 二叉搜索树的最近公共祖先

## 题目
给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

最近公共祖先的定义为: "对于有根树 T 的两个结点 p、q, 最近公共祖先表示为一个结点 x, 满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。"

例如,给定如下二叉搜索树: root = [6,2,8,0,4,7,9,null,null,3,5]

示例 1:
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。

示例 2:
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先可以为节点本身。

说明:
- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉搜索树中。

## 思路

1. 由于二叉搜索树的特性,我们可以利用它的性质来解决这个问题。
2. 如果 `p` 和 `q` 的值都小于 `root` 的值,说明它们都在 `root` 的左子树中,我们可以递归地在左子树中查找最近公共祖先。
3. 如果 `p` 和 `q` 的值都大于 `root` 的值,说明它们都在 `root` 的右子树中,我们可以递归地在右子树中查找最近公共祖先。
4. 如果 `p` 和 `q` 的值在 `root` 的两侧,说明 `root` 就是最近公共祖先,我们直接返回 `root`。

**代码分析**:
1. 首先,我们判断 `root` 是否为空或者等于 `p` 或 `q`,如果是,我们直接返回 `root`。
2. 然后,我们判断 `p` 和 `q` 的值是否都小于 `root` 的值,如果是,我们递归地在左子树中查找最近公共祖先。
3. 接下来,我们判断 `p` 和 `q` 的值是否都大于 `root` 的值,如果是,我们递归地在右子树中查找最近公共祖先。
4. 如果以上两种情况都不满足,说明 `p` 和 `q` 的值在 `root` 的两侧,我们直接返回 `root`。

## 代码

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // 1. 如果 root 为空或者等于 p 或 q,直接返回 root
        if (root == null || root == p || root == q) {
            return root;
        }

        // 2. 如果 p 和 q 的值都小于 root 的值,说明它们在 root 的左子树中,递归左子树
        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        }

        // 3. 如果 p 和 q 的值都大于 root 的值,说明它们在 root 的右子树中,递归右子树
        if (p.val > root.val && q.val > root.val) {
            return lowestCommonAncestor(root.right, p, q);
        }

        // 4. 如果 p 和 q 的值在 root 的两侧,说明 root 就是最近公共祖先,返回 root
        return root;
    }
}
```

## 效率

- 时间复杂度: O(log n),其中 n 为二叉搜索树的节点数。在最坏情况下,我们需要遍历从根节点到叶子节点的路径,这个路径的长度最多为树的高度,即 O(log n)。
- 空间复杂度: O(1),我们只使用了常量级的额外空间。

