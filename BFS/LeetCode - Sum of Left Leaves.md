## **LeetCode > Breadth-First Search > Sum of Left Leaves**

</br>

[연습 문제 링크](https://leetcode.com/problems/sum-of-left-leaves/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

</br>

## 영어 지문

Given the root of a binary tree, return the sum of all left leaves.

</br>

## 예시

![left-sum](https://user-images.githubusercontent.com/75058239/137571690-f85f10b1-f8a5-4df9-ba69-b61c29c892fb.png)

</br>

## 추가 사항

- The number of nodes in the tree is in the range [1, 1000].
- -1000 <= Node.val <= 1000

</br>

## 문제 요약

이진 트리의 root가 주어진다.  
모든 왼쪽 노드들의 합을 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=g16fLbVcK0U&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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
    int sum = 0;

    public int sumOfLeftLeaves(TreeNode root) {
        if (root != null) traverse(root);
        return sum;
    }

    public boolean traverse(TreeNode root) {
        if (root.left != null) {
            boolean isLeaf = traverse(root.left);
            if (isLeaf) sum += root.left.val;
        }
        if (root.right != null) traverse(root.right);
        return root.left == null && root.right == null;
    }
}
```

재귀적인 구현 방식이다.  
재귀 함수를 boolean 타입으로 지정해줌으로서, 재귀 함수가 호출될 때마다 더이상의 자식이 없는 왼쪽 노드인지에 대한 유효성을 판단한다.  
더이상의 자식이 없는 왼쪽 노드라면, 최상위에 지정해둔 변수에 그 값을 더해주어서 값을 최신화한다.
