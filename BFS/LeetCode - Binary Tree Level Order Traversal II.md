## **LeetCode > Breadth-First Search / Binary Tree > Binary Tree Level Order Traversal II**

</br>

[연습 문제 링크](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Medium

</br>

## 영어 지문

Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

</br>

## 예시

![Binary Tree Level Order Traversal II 예시](https://user-images.githubusercontent.com/75058239/128592252-1407f44b-200a-40af-88d4-8fba2d9b14b7.png)

</br>

## 추가 사항

- The number of nodes in the tree is in the range [0, 2000].
- -1000 <= Node.val <= 1000

</br>

## 문제 요약

Binary Tree의 root가 주어진다.  
leaf에서부터 root까지 오면서, 해당 level의 왼쪽과 오른쪽 값을 배열에 담고, 각 레벨의 배열들이 담긴 배열을 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=3InqyEPZsw0&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while(!q.isEmpty()) {
            List<Integer> level = new ArrayList<>();
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                level.add(node.val);
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            result.add(0, level);
        }

        return result;
    }
}
```

BFS 문제를 풀 때는 Queue를 활용해야 한다는 사실을 다시 한번 명심하자.  
풀이를 살펴보자면, for문 안에서 q의 size만큼 돌면서 node의 값들을 각 레벨 배열에 담아준다.  
동시에 해당 node의 왼쪽 값과 오른쪽 값을 q에 넣어준다.  
그리고 각 for문을 통해 얻은 level 배열을 그대로 result에 add하면 문제에서 요구하는 아래에서부터 위로 올라가는 방식이 아닌, 위에서부터 아래로 쌓이게 되니, 승지니어 님은 센스 있게 result의 0번째 인덱스에 level을 넣어주는 방식으로 문제를 해결했다.  
이러한 작업을 q가 비어있을 때까지 반복하면서 리턴할 배열을 만들어주는 것이다.

</br>

## 소감

이제 조금은 핵심 유형들의 문제 풀이 방법에 대해서 가닥을 잡아가고 있는 느낌이 들기는 한다.  
하지만 뭔가··· 다분히 추상적인 느낌으로 이해가 되는 느낌이다.  
대강 어떤 느낌인지는 감이 잡히는데, 값이 정확히 어떤 시점에 어떻게 변하고 어떻게 결과값이 도출될 수 있는지, 그 정확한 연산 과정이 머릿 속에 그려지지는 않는다.  
역시 아직은 테스트 케이스가 들어와서 통과하기 까지의 과정을 직접 그려보거나 하지 않으면 안되겠다는 생각이 든다.
