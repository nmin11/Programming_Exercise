## **LeetCode > Breadth-First Search > ㅡ**

</br>

[연습 문제 링크](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

</br>

## 영어 지문

Given a n-ary tree, find its maximum depth.  
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.  
Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

</br>

## 예시

![maximum-depth-of-n-ary-tree-1](https://user-images.githubusercontent.com/75058239/135811272-57600620-9fd7-420a-aee4-e6b5be9cf4b6.png)

**Input:** root = [1,null,3,2,4,null,5,6]

</br>

![maximum-depth-of-n-ary-tree-2](https://user-images.githubusercontent.com/75058239/135811287-78df95d2-eb0d-4796-ac94-00f3b887b6e0.png)

**Input:** root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]

</br>

## 추가 사항

- The total number of nodes is in the range [0, 10⁴].
- The depth of the n-ary tree is less than or equal to 1000.

</br>

## 문제 요약

n-ary 트리가 주어진다.  
이것의 최대 깊이를 찾아라.  
최대 깊이는 root node에서 leaf node까지 가능한 한 가장 긴 경로로 이어지는 최대 node 수이다.  
input 값인 Nary-Tree의 직렬화는 레벨 순서 순회 방식으로 표현되며, 각 자식 그룹 간의 구분은 null 값으로 한다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=t1NkSkVHcnA&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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

class Solution {
    public int maxDepth(Node root) {
        if (root == null) return 0;
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        int depth = 0;

        while (!q.isEmpty()) {
            depth++;
            int size = q.size();
            for (int i = 0; i < size; i++) {
                Node node = q.poll();
                for (Node child : node.children) {
                    q.offer(child);
                }
            }
        }

        return depth;
    }
}
```
