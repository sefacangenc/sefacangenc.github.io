---
title: "How to Determine if a Binary Tree is Height-Balanced using Python"
description: "This tutorial explains how to find the diameter of a binary tree using depth-first search (DFS) algorithm in Python. It includes a step-by-step example to illustrate the process of traversing the tree and calculating the diameter."
pubDate: "Apr 10 2023"
heroImage: "/posts-jpg/balanced-binary-tree.jpg"
layout: ../../layouts/BlogPost.astro

---

A balanced binary tree is a binary tree in which the height of the two subtrees of any node never differ by more than one. In other words, a binary tree is height-balanced if for each node in the tree, the difference in the height of the left and right subtrees is at most one.

In this blog post, we'll discuss a Python algorithm to determine if a given binary tree is height-balanced. We'll explain the algorithm step-by-step and provide examples along the way.

The Algorithm

Our algorithm will use a recursive approach to check if the tree is height-balanced. We'll define a helper function called dfs that takes in a node and returns a list of two values. The first value will be a boolean indicating whether the subtree rooted at this node is height-balanced, and the second value will be an integer representing the height of the subtree rooted at this node.

Here's the Python code for our algorithm:
```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]

            left, right = dfs(root.left), dfs(root.right)
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, 1 + max(left[1], right[1])]

        return dfs(root)[0]
```
Let's go through the algorithm step-by-step.

Step 1: Define the dfs helper function
As mentioned above, we'll define a helper function called dfs that takes in a node and returns a list of two values. If the node is None (i.e., it doesn't exist), we'll return a list with a boolean value of True (since an empty tree is always height-balanced) and a height of 0. Here's the code:

```python
def dfs(root):
    if not root:
        return [True, 0]

```


Step 2: Recursively call dfs on left and right subtrees
If the node exists, we'll recursively call dfs on its left and right subtrees. This will give us two lists, left and right, each containing a boolean value indicating whether the subtree rooted at that node is height-balanced, and an integer representing the height of the subtree rooted at that node. Here's the code:

```python
left, right = dfs(root.left), dfs(root.right)
```
Step 3: Check if the current node is height-balanced
Now that we have the results from dfs for the left and right subtrees, we can check if the current node is height-balanced. To do this, we'll first check if the left subtree, right subtree, and the difference in their heights are all within one of each other. We'll store the result in a boolean variable called balanced. Here's the code:

```python
balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
```

Step 4: Calculate the height of the current subtree
Finally, we'll calculate the height of the current subtree by taking the maximum height of the left and right subtrees and adding one (to account for the current node). We'll store the result in a list with the balanced variable as the first value and the height of the current subtree as the second value. Here's the code:


```python
return [balanced, 1 + max(left[1], right[1])]
```
Overall the final code:

This code defines a class Solution with a single method isBalanced that takes in a binary tree represented as a TreeNode object and returns a boolean indicating whether the tree is height-balanced or not. The method uses a helper function dfs to perform a depth-first search on the tree.

The dfs function takes in a TreeNode object and returns a list with two elements: a boolean indicating whether the tree rooted at the input node is height-balanced, and an integer indicating the height of the tree rooted at the input node. If the input node is None, the function returns [True, 0], indicating that an empty tree is height-balanced and has height 0.

If the input node is not None, the function makes recursive calls to dfs on the left and right children of the node, and stores the results in the left and right variables, respectively. The balanced variable is then computed by checking if the left and right subtrees are height-balanced, and if the absolute difference in their heights is at most 1. Finally, the function returns a list with two elements: balanced and the height of the current node, which is computed as 1 plus the maximum of the heights of the left and right subtrees.

The isBalanced method simply calls dfs on the root of the input tree, and returns the first element of the resulting list, which indicates whether the entire tree is height-balanced or not.

This algorithm has a time complexity of O(n), where n is the number of nodes in the tree, since each node is visited exactly once. The space complexity is also O(n), since the depth of the recursion can be at most n for a skewed tree, and each recursive call requires O(1) space.

```py
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]

            left, right = dfs(root.left), dfs(root.right)
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, 1 + max(left[1], right[1])]

        return dfs(root)[0]
```