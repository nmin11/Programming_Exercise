## **LeetCode > Binary Search Tree > Kth Smallest Element in a BST**

</br>

[연습 문제 링크](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

</br>

## 추가 사항

- 1 <= k <= n <= 10⁴
- 0 <= Node.val <= 10⁴

</br>

## 문제 요약

Binary Search Tree의 root가 주어지고, 정수 k가 주어진다.  
Tree의 모든 node의 값들 중 k번째로 작은 숫자를 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=uz8Ivl0uTAw&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int k;
    int i;
    int result;
    public int kthSmallest(TreeNode root, int k) {
        this.k = k;
        i = 0;
        traverse(root);
        return result;
    }

    public boolean traverse(TreeNode root) {
        if (root == null) return false;
        boolean b = traverse(root.left);
        if (b) return b;
        if (++i == k) {
            result = root.val;
            return true;
        }
        return traverse(root.right);
    }
}
```

Binary Search Tree를 inorder 방식으로 순회하면 알아서 오름차순으로 정렬된 배열을 얻을 수 있다.  
그리고, boolean 타입을 활용해서 순회 과정을 조금 더 최적화했다.
