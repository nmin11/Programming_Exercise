## **LeetCode > Tree > Symmetric Tree**

<br>

[연습 문제 링크](https://leetcode.com/problems/symmetric-tree/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

<br>

## 영어 지문

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

<br>

## 예시

(이미지 첨부 1)

**Input:** root = [1,2,2,3,4,4,3]  
**Output:** true

<br>

(이미지 첨부 2)

**Input:** root = [1,2,2,null,3,null,3]  
**Output:** false

<br>

## 추가 사항

- The number of nodes in the tree is in the range [1, 1000].
- -100 <= Node.val <= 100

<br>

## 문제 요약

이진 트리의 루트가 주어진다.  
트리가 거울 형태를 띄는지 확인하라. (즉, 중심을 기준으로 대칭이 되는지)

<br>

## [승지니어 님의 풀이](https://youtu.be/yAUqLfuPSP8)

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return compare(root.left, root.right);
    }

    public boolean compare(TreeNode a, TreeNode b) {
        if (a == null && b == null) return true;
        if (a == null || b == null) return false;
        if (a.val != b.val) return false;

        return compare(a.left, b.right) && compare(a.right, b.left);
    }
}
```

아직도 트리를 다루는 일이 익숙치 않음을 느낀다.  
그래도 다행히 승지니어 님의 로직이 어떤 양상으로 문제를 풀어나가는지 감을 잡을 수는 있었지만, 내가 이런 로직을 직접 구현하라면 아쉽게도 못 할 것 같다.  
좋은 로직을 보고 배우는 데에 그치지 말고, 관련된 문제를 더 많이 풀어보도록 하자.
