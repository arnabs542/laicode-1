## Symmetric Binary Tree

[https://app.laicode.io/app/problem/48](https://app.laicode.io/app/problem/48)

## Description

Check if a given binary tree is symmetric.

Examples

            5

          /    \

        3        3

      /   \    /   \

    1      4  4      1

is symmetric.

            5

          /    \

        3        3

      /   \    /   \

    1      4  1      4

is not symmetric.

Corner Cases

- What if the binary tree is null? Return true in this case.

How is the binary tree represented?

We use the level order traversal sequence with a special symbol "#" denoting the null node.

For Example:

The sequence \[1, 2, 3, #, #, 4\] represents the following binary tree:

        1

      /   \

     2     3

          /

        4

Easy

Binary Tree

## Assumption

The tree is not null or empty.

## Algorithm

- Use a helper function which takes two nodes (root nodes of the original root's left and right child respectively)
- Assumption ⇒ null is symmetric
- Compare the two subtrees/nodes, see if they have the same key
- Recursively check
  - the _left child_ of the _left subtree_ & the _right child_ of the _right subtree_
  - the _right child_ of the _left subtree_ & the _left child_ of the _right subtree_

## Solution

### Code

```java
public class Solution {

  public boolean isSymmetric(TreeNode root) {
    // Write your solution here
    if (root == null) {
      return true;
    }
    // Recursively check the left and right subtrees
    return isSymmetricBinaryTree(root.left, root.right);
  }

  private boolean isSymmetricBinaryTree(TreeNode left, TreeNode right) {
    // Case 1: if both of the nodes are null ==> symmetric
    // Case 2: if either of the nodes is null ==> asymmetric
    // Case 3: if both of the nodes are not null, but the keys are different ==> assymetric
    if (left == null && right == null) {
      return true;
    } else if (left == null || right == null) {
      return false;
    } else if (left.key != right.key) {
      return false;
    }
    // Recursively check
    // 1. the left child of left subtree with the right child of right subtree
    // 2. the right child of left subtree with the left child of right subtree
    return (
      isSymmetricBinaryTree(left.left, right.right) &&
      isSymmetricBinaryTree(left.right, right.left)
    );
  }
}
```

### Complexity

Time: we need to check all n nodes ⇒ O(n)

Space: recursion tree depends on the height of the tree ⇒ O(height)
