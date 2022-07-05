# Technical-Interview-Topics

## Contents

- [Binary Search](#binary-search)
- [Breadth First Search](#breadth-first-search)
- [Depth First Search](#depth-first-search)
- [Backtracking](#backtracking)
- [Dynamic Programming](#dynamic-programming)
- [Binary Tree Traversal](#binary-tree-traversal)
- [Recursion (Top Down Approach)](#recursion-(top-down-approach))
- [Recursion + Memorization (Top Down Approach)](#recursion-+-memorization-(top-down-approach))
- [DP (Bottom Up Approach)](#dP-(bottom-up-approach))
- [DP + Optimization (Bottom Up Approach)](#dP-+-optimization-(bottom-up-approach))




## Binary Search
```js
int i = 0, j = n-1;
while(i <= j) {
    int m = i + (j-i) / 2;
    if(arr[m] == target) {
        return m;
    } else if(arr[m] < target) {
        i = m+1;
    } else {
        j = m-1;
    }
}
```

## Breadth First Search
```js
boolean[] visited = new boolean[n];
Deque<Integer> queue = new LinkedList();
queue.offer(0);
while(!queue.isEmpty()) {
    int x = queue.poll();
    // do something to generate the output of your algorithm
    // or just return x if that's what you are searching for
    visited[x] = true;
    int[] nextElements = getElementsAssessibleFromX(x);
    for(int y: nextElements) {
        if(!visited[y]) {
            queue.offer(y);
        }
    }
}
```

## Depth First Search
```js
// Just replace the queue in BFS with stack and you are done:
boolean[] visited = new boolean[n];
Deque<Integer> stack = new LinkedList();
stack.push(0);
while(!stack.isEmpty()) {
    int x = stack.pop();
    // do something to generate the output of your algorithm
    // or just return x if that's what you are searching for
    visited[x] = true;
    int[] nextElements = getElementsAssessibleFromX(x);
    for(int y: nextElements) {
        if(!visited[y]) {
            stack.push(y);
        }
    }
}
```

## Backtracking
```js
// Generally a recursive algorithm attempting candidates and either accepting them or rejecting (“backtracking”) based on some condition.
// Below is an example of permutations generation using backtracking:

public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> ans = new ArrayList<>();
    backtrack(ans, new ArrayList<Integer>(), nums);
    return ans;
}
private void backtrack(List<List<Integer>> ans, List<Integer> ongoing, int[] nums) {
    if(ongoing.size() == nums.length) {
        ans.add(new ArrayList<>(ongoing));
    } else {
        for(int i = 0; i < nums.length; i++) {
            if(!ongoing.contains(nums[i])) {
                ongoing.add(nums[i]);
                backtrack(ans, ongoing, nums);
                ongoing.remove(ongoing.size() - 1);
            }
        }
    }
}
```
## Dynamic Programming
```js
// Technique to determine result using previous results. You should be able to reason about your solution 
// recursively and be able to deduce dp[i] using dp[i-1]. Generally you would have something like this:

int[] dp = new int[n];
dp[0] = // something that makes sense for initial value
for(int i = 1; i < n; ++i) {
  dp[i] = // some way to get value using dp[i-1]
}
return dp[n-1];
```
## Binary Tree Traversal
```js
// Inorder: left-root-right
// Postorder: left-rigth-root
// Preorder: root-left-right
// Plus each one of them could have reverse for right and left
// Below are recursive and iterative versions of inorder traversal

// recursive
public List<Integer> inorderTraversal(TreeNode root) {
  List<Integer> ans = new ArrayList();
  if(root == null) return ans;
  ans.addAll(inorderTraversal(root.left));
  ans.add(root.val);
  ans.addAll(inorderTraversal(root.right));
  return ans;
}

// iterative
public List<Integer> inorderTraversal(TreeNode root) {
  List<Integer> ans = new ArrayList();
  Deque<TreeNode> stack = new LinkedList();
  while(root != null || !stack.isEmpty()) {
    while(root != null) {
      stack.push(root);
      root = root.left;
    }
    root = stack.pop();
    ans.add(root.val);
    root = root.right;
  }
  return ans;
}
```

## Recursion (Top Down Approach)
```js

/**
 * Question   : Climbing Stairs
 * Complexity : Time: O(2^n) ; Space: O(n)
 */
class Solution {
    public int climbStairs(int n) {
        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        return climbStairs(n - 1) + climbStairs(n - 2);
    }
}
```

## Recursion + Memorization (Top Down Approach)
```js
/**
 * Question   : Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public int climbStairs(int n) {
        Map<Integer, Integer> memo = new HashMap<>();
        memo.put(1, 1);
        memo.put(2, 2);
        return climbStairs(n, memo);
    }

    private int climbStairs(int n, Map<Integer, Integer> memo) {
        if (memo.containsKey(n)) {
            return memo.get(n);
        }
        memo.put(n, climbStairs(n - 1, memo) + climbStairs(n - 2, memo));
        return memo.get(n);
    }
}
```

## DP (Bottom Up Approach)

```js
/**
 * Question   : Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public int climbStairs(int n) {
        if (n <= 1) {
            return 1;
        }
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;

        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

## DP + Optimization (Bottom Up Approach)

```js
/**
 * Question   : Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    public int climbStairs(int n) {
        if (n <= 1) {
            return 1;
        }

        int prev1 = 1;
        int prev2 = 2;

        for (int i = 3; i <= n; i++) {
            int newValue = prev1 + prev2;
            prev1 = prev2;
            prev2 = newValue;
        }

        return prev2;
    }
}
```

















