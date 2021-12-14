## **LeetCode > Depth-First Search > N-ary Tree Preorder Traversal**

<br>

[연습 문제 링크](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

<br>

## 영어 지문

Given the `root` of an n-ary tree, return _the preorder traversal of its nodes' values._

Nary-Tree input serialization is represented in their level order traversal.
Each group of children is separated by the null value.

<br>

## 예시

![maximum-depth-of-n-ary-tree-1](https://user-images.githubusercontent.com/75058239/135811272-57600620-9fd7-420a-aee4-e6b5be9cf4b6.png)

**Input:** root = [1,null,3,2,4,null,5,6]  
**Output:** root = [1,3,5,6,2,4]

<br>

![maximum-depth-of-n-ary-tree-2](https://user-images.githubusercontent.com/75058239/135811287-78df95d2-eb0d-4796-ac94-00f3b887b6e0.png)

**Input:** root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]  
**Output:** root = [1,2,3,6,7,11,14,4,8,12,5,9,13,10]

<br>

## 추가 사항

- The number of nodes in the tree is in the range `[0, 10⁴]`.
- 0 <= `Node.val` <= 10⁴
- The height of the n-ary tree is less than or equal to `1000`.

<br>

## 문제 요약

n-ary 트리의 `root`가 주어진다.  
preorder 방식으로 순회한 노드 값들을 리턴하라.

N-ary 입력 순서는 레벨 순서 순회 방식으로 입력된다.  
각 자식들의 그룹은 null 값에 의해 구분된다.

<br>

## [승지니어 님의 풀이](https://youtu.be/jHSoaw0pFe4)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

/*
preorder : self - children
postorder : children - self
*/

class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> result = new ArrayList<>();
        traverse(root, result);
        return result;
    }

    public void traverse(Node root, List<Integer> result) {
        if (root == null) return;
        result.add(root.val);
        for (Node child : root.children) {
            traverse(child, result);
        }
    }
}
```
