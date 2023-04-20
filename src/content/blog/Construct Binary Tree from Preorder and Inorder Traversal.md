---
title: "Constructing Binary Tree from Preorder and Inorder Traversals in Python"
description: "Learn how to construct a binary tree from its preorder and inorder traversals using a recursive algorithm in Python, with step-by-step explanation and code."
pubDate: "Apr 20 2023"
heroImage: "/"
---
Construct Binary Tree from Preorder and Inorder Traversal
Given the preorder and inorder traversals of a binary tree, we can construct the tree using a recursive algorithm. The basic idea is as follows:

The first element of the preorder traversal is the root node of the tree.
We can find the root node in the inorder traversal, which splits the inorder traversal into left and right subtrees.
We can use the length of the left subtree to split the preorder traversal into left and right subtrees.
We can then recursively build the left and right subtrees.
Let's take the example of the following binary tree:

```m
     3
   /   \
  9    20
      /  \
     15   7
```
The preorder traversal of the tree is [3, 9, 20, 15, 7], and the inorder traversal is [9, 3, 15, 20, 7].

Python Implementation
Here's how we can implement the above algorithm in Python:

```py
class Solution:
    def buildTree(self, preorder, inorder):
        if not preorder or not inorder:
            return None

        # The first element of preorder is the root node
        root_val = preorder.pop(0)
        root = TreeNode(root_val)

        # Find the index of the root node in inorder
        root_idx = inorder.index(root_val)

        # Recursively build left and right subtrees
        root.left = self.buildTree(preorder, inorder[:root_idx])
        root.right = self.buildTree(preorder, inorder[root_idx + 1:])

        return root
```

Example
Let's see how the algorithm works for the example binary tree we used above:
```py
s = Solution()
root = s.buildTree([3, 9, 20, 15, 7], [9, 3, 15, 20, 7])
```

Initially, the preorder and inorder traversals are [3, 9, 20, 15, 7] and [9, 3, 15, 20, 7], respectively. We create the root node with value 3, and then split the inorder traversal into [9] and [15, 20, 7], indicating the left and right subtrees, respectively. We also split the preorder traversal into [9, 20, 15, 7] and [15, 7].

We then recursively call the buildTree method for the left subtree, passing the [9, 20] and [9] sub-arrays of the preorder and inorder traversals, respectively. In this call, we create a node with value 9 and assign it to the left attribute of the current node.

Next, we recursively call the buildTree method for the right subtree, passing the [20, 15, 7] and [15, 20, 7] sub-arrays of the preorder and inorder traversals, respectively. In this call, we create a node with value 20, assign it to the right attribute of the current node, and then create a node with value 15 and assign it to the left attribute of the 20 node. Finally, we create a node with value 7 and assign it to the right attribute of the 20 node