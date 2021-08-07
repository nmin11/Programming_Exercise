## **LeetCode > Binary Search Tree > Minimum Absolute Difference in BST**

</br>

[연습 문제 링크](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 영어 지문

Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

</br>

## 추가 사항

- The number of nodes in the tree is in the range [2, 10⁴].
- 0 <= Node.val <= 10⁵

</br>

## 문제 요약

Binary Search Tree의 root가 주어진다.  
Tree에서 2개의 노드의 값을 가지고 뺄셈을 했을 때, 뺄셈 결과의 최솟값을 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=KLX44z_NnYc&t=300s&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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
    /*
    트리 순회(재귀) :
    preorder : self left right
    inorder : left self right
    postorder : left right self
    이진 탐색 트리는 inorder => 알아서 오름차순 정렬이 됨
    */
    boolean init;
    int min;
    int prev;
    public int getMinimumDifference(TreeNode root) {
        init = false;
        min = Integer.MAX_VALUE;
        inorder(root);
        return min;
    }

    public void inorder(TreeNode root) {
        if (root == null) return;
        inorder(root.left);
        //self 처리
        if (!init) {
            init = true;
        } else {
            min = Math.min(min, root.val - prev);
        }
        prev = root.val;
        inorder(root.right);
    }
}
```

승지니어 님이 영상에서 무척 간단하게 풀어내셨지만 나는 이해하는 데에 꽤나 시간이 걸렸다.  
풀이를 간단히 살펴보자면, 우선 주석으로도 달려 있듯이, 이진 탐색 트리는 inorder에 맞게 탐색하면 알아서 오름차순 정렬이 되는 탐색 방법이다.  
이에 맞게 inorder를 재귀 호출하는 방식으로 간단하게 해결해주었다.  
재귀 함수 안에서 root, 즉 자기 자신을 만난 조건에 한해서 처음에는 우선 init을 통해 자기 자신에게 들어왔음을 표시하는 작업을 한다.  
만약, 자기 자신을 한번 더 방문한 경우라면, 기존의 최솟값과 root.val - prev 값을 비교하여 더 작은 값을 최솟값에 할당해주는 것이다.

</br>

## 소감

최근, 코드스테이츠에서 제공해준 정말 까다로운 Algorithm 50문제를 풀고 있다.  
그렇게 문제를 풀다보니 들게 된 생각이, **'Algorithm이 너무 방대하고 풀 문제들도 많다고 해서 괜히 기 꺾이지 말고, 정말 핵심적인 Algorithm 풀이 기법을 차근차근 익혀가면서 물고기 잡는 방법을 익히자!'** 는 생각이었다.  
물론 아직도 잘 모르는 Algorithm의 핵심 원리들이 많지만, 근래 Algorithm 문제 유형이나 핵심 개념들을 살펴보다 보니, 정말 자주 출제되고, 꼭 알아두어야 하는 개념들이 존재한다는 것을 깨달았다.  
그렇기에, 무작정 문제를 풀어나가기 보다는, 특정 Algorithm 유형에는 어떤 풀이 기법이 있는지를 좀 더 상세하게 파헤쳐 보고 있다.  
오늘도 글을 올리게 된 이진 탐색 트리, 개념적으로는 알고 있었지만, 이를 코드로 구현하려니 턱 막히고 답답했다.  
하지만 이렇게 풀이 영상을 보니 문제에 접근하는 풀이 방법에 대해서 어느 정도 깨우친 바가 있다.  
이와 같이, 당분간은 새 문제를 풀기보다는 이런식으로 **'급할수록 돌아가라'** 는 전법을 활용하게 될 것 같다.
