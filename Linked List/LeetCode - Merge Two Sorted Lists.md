## **LeetCode > Linked List / Recursion > Merge Two Sorted Lists**

</br>

[연습 문제 링크](https://leetcode.com/problems/merge-two-sorted-lists/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 영어 지문

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

</br>

## 예시

(이미지 첨부)

</br>

## 추가 사항

- The number of nodes in both lists is in the range [0, 50].
- -100 <= Node.val <= 100
- Both l1 and l2 are sorted in **non-decreasing** order.

</br>

## 문제 요약

두개의 정렬된 Linked List들을 병합하고, 이를 **정렬**해서 반환하라.  
배열은 처음 두 노드를 함께 연결하면서 만들어져야 한다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=t4c-fkpycVA&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode result = null;
        ListNode current = null;

        while (l1 != null || l2 != null) {
            if (l2 == null || (l1 != null && l1.val < l2.val)) {
                //pick from l1
                if (result == null) {
                    result = l1;
                    current = l1;
                    l1 = l1.next;
                } else {
                    current.next = l1;
                    current = l1;
                    l1 = l1.next;
                }
            } else {
                //pick from l2
                if (result == null) {
                    result = l2;
                    current = l2;
                    l2 = l2.next;
                } else {
                    current.next = l2;
                    current = l2;
                    l2 = l2.next;
                }
            }
        }

        return result;
    }
}
```

중복 코드가 있지만 이렇게 두는 것이 더 가독성이 있기에 이렇게만 짜두었다.  
while문 안쪽에서 두 값이 null이 아닐 때, 둘 중 작은 값을 가져오는 방식으로 작성되었다.  
사실 ListNode를 활용해서 로직을 수행하는 과정이 익숙하지 않아서 이해가 잘 되지는 않았지만 두고두고 보면서 차근차근 이해를 해야만 하겟다.
