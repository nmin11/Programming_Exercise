## **LeetCode > Binary Search Tree > Binary Search Tree Iterator**

<br>

[연습 문제 링크](https://leetcode.com/problems/binary-search-tree-iterator/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

<br>

## 영어 지문

Implement the `BSTIterator` class that represents an iterator over the **in-order traversal** of a binary search tree (BST):

- `BSTIterator(TreeNode root)` Initializes an object of the `BSTIterator` class.<br>The `root` of the BST is given as part of the constructor.<br>The pointer should be initialized to a non-existent number smaller than any element in the BST.
- `boolean hasNext()` Returns `true` if there exists a number in the traversal to the right of the pointer, otherwise returns `false`.
- `int next()` Moves the pointer to the right, then returns the number at the pointer.

<br>

## 예시

(이미지 첨부 bst-iterator)

**Input**

["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]  
[[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]

<br>

**Output**

[null, 3, 7, true, 9, true, 15, true, 20, false]

<br>

**Explantaion**

```java
BSTIterator iterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
iterator.next();        //return 3
iterator.next();        //return 7
iterator.hasNext();     //return true
iterator.next();        //return 9
iterator.hasNext();     //return true
iterator.next();        //return 15
iterator.hasNext();     //return true
iterator.next();        //return20
iterator.hasNext();     //return false
```

<br>

## 추가 사항

- The number of nodes in the tree is in the range [1, 10⁵].
- 0 <= Node.val <= 10⁶
- At most 10⁵ calls will be made to hasNext, and next.

<br>

## 문제 요약

이진 탐색 트리(BST)를 in-order 방식으로 순회하는 반복자 `BSTIterator` 클래스 구현:

- `BSTIterator(TreeNode root)` : `BSTIterator` 클래스의 객체를 초기화한다.<br>생성자의 매개 변수로 BST의 `root`가 주어진다.<br>포인터는 BST의 어떤 숫자보다도 작은 숫자로 초기화되어야 한다.
- `boolean hasNext()` : 포인터의 오른쪽에 값이 있으면 `true`를, 그렇지 않다면 `false`를 리턴한다.
- `int next()` : 포인터를 오른쪽으로 이동하고, 포인터의 숫자를 리턴한다.

<br>

## [승지니어 님의 풀이](https://youtu.be/5gFeBx5JtiM)

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

/*
BST : 왼쪽 sub-tree는 나보다 작고, 오른쪽 sub-tree는 나보다 크고
BST를 in-order 순회하면 결국 오름차순 정렬된 값 반환
*/

class BSTIterator {
    Stack<TreeNode> stack = new Stack<>();

    public BSTIterator(TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }

    public int next() {
        TreeNode node = stack.pop();
        if (node.right != null) {
            TreeNode cur = node.right;
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
        }

        return node.val;
    }

    public boolean hasNext() {
        return !stack.isEmpty();
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```
