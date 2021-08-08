## **LeetCode > Linked List / Two Pointers > Middle of the Linked List**

</br>

[연습 문제 링크](https://leetcode.com/problems/middle-of-the-linked-list/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 영어 지문

Given the head of a singly linked list, return the middle node of the linked list.  
If there are two middle nodes, return **the second middle** node.

</br>

## 추가 사항

- The number of nodes in the list is in the range [1, 100].
- 1 <= Node.val <= 100

</br>

## 문제 요약

Linked List인 head가 주어진다.  
Linked List의 가운데 노드부터 끝까지를 배열로 리턴하라.  
만약 가운데 노드들이 2개라면 2개 중, **2번째 노드**부터 끝까지를 리턴하라.

</br>

## 예시

(이미지 첨부)

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=ucJ1XhM6EEU&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */

// 위에 주어져 있는 ListNode를 살펴보면 size가 주어져 있지 않다.

/* 쉬운 방법
1. iteration 돌면서 size 측정
2. size를 바탕으로 중간 노드 이후 범위부터
두번째 iteration 돌면서 중간 노드를 반환
*/

/* walker runner 테크닉 활용 방법
warker : 한번에 한칸씩
runner : 한번에 두칸씩
runner가 끝나면 walker는 중간에 와있음
*/

class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode walker = head;
        ListNode runner = head;

        while (runner != null) {
            runner = runner.next;
            if (runner != null) {
                walker = walker.next;
                runner = runner.next;
            }
        }
        return walker;
    }
}
```

walker / runner 테크닉에 대해 배워갈 수 있었다.  
실상 간단한 테크닉이었지만 기발하다는 생각이 들었고, 추후에 이 테크닉을 꼭 다시 써먹어봐야겠다.
