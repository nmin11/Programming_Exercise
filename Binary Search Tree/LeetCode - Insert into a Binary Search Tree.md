## **LeetCode > Binary Search Tree > Insert into a Binary Search Tree**

<br>

[연습 문제 링크](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

<br>

## 영어 지문

You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree.  
Return _the root node of the BST after the insertion._  
It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion.  
You can return any of them.

<br>

## 예시

(이미지 첨부 insertbst)

**Input** : root = [4,2,7,1,3], val = 5  
**Output** : [4,2,7,1,3,5]  
**Explanation** : Another accepted tree is

(이미지 첨부 insertbst2)

<br>

**Input** : root = [40,20,60,10,30,50,70], val = 25  
**Output** : [40,20,60,10,30,50,70,null,null,25]

<br>

**Input** : root = [4,2,7,1,3,null,null,null,null,null,null], val = 5  
**Output** : [4,2,7,1,3,5]

<br>

## 추가 사항

- The number of nodes in the tree will be in the range [0, 10⁴].
- -10⁶ <= `Node.val` <= 10⁶
- All the values `Node.val` are **unique**
- -10⁶ <= `val` <= 10⁶
- It's **guaranteed** that `val` does not exist in the original BST.

<br>

## 문제 요약

BST의 `root` 노드와 이 트리에 삽입할 `value`가 주어진다.  
삽입 과정 이후 BST의 root 노드를 반환하라.  
추가하게 될 값은 기존의 BST에는 없던 값이라는 게 보장된다.

삽입 후 트리가 BST로 유지될 수 있는 한, 여러 개의 유효한 경우의 수가 있을 수 있음을 명심하라.  
여러 가지 경우의 수 중 아무거나 반환해도 된다.

<br>

## [승지니어 님의 풀이](https://youtu.be/GBZw0I3I1jw)

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);

        TreeNode child = null;

        if(val > root.val) {
            child = insertIntoBST(root.right, val);
            root.right = child;
        } else {
            child = insertIntoBST(root.left, val);
            root.left = child;
        }

        return root;
    }
}
```
