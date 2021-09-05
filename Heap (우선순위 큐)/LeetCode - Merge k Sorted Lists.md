## **LeetCode > Linked List, Heap (Priority Queue), Merge Sort > Merge k Sorted Lists**

</br>

[연습 문제 링크](https://leetcode.com/problems/merge-k-sorted-lists/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Hard

</br>

## 영어 지문

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.  
_Merge all the linked-lists into one sorted linked-list and return it._

</br>

## 추가 사항

- k == lists.length
- 0 <= k <= 10⁴
- 0 <= lists[i].length <= 500
- -10⁴ <= lists[i][j] <= 10⁴
- lists[i] is sorted in **ascending order**.
- The sum of lists[i].length won't exceed 10⁴.

</br>

## 문제 요약

k개의 linked-list들이 주어지며 각 linked-list들은 오름차순 정렬이 되어 있다.  
모든 linked-list들을 하나로 병합하여 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=DjMLYwtSp08&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

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

//external sort
/*
list.size → k, pq에는 각 리스트의 첫번째 원소 삽입 (초기화)
while pq is not empty
ListNode min = extractMin(pq) → 출력, pq.offer(min.next);
*/
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        ListNode result = null;
        ListNode current = null;

        //min heap
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.length,
                                    /*comparator*/(a, b) -> a.val - b.val);

        for (ListNode node : lists) {
            if (node == null) continue;
            pq.offer(node);
        }

        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            if (node.next != null) pq.offer(node.next);
            if (result == null) {
                result = node;
                current = node;
            } else {
                current.next = node;
                current = node;
            }
        }

        return result;
    }
}
```

우선, PriorityQueue를 선언할 때, 생성자에 기본 크기와 정렬 메소드를 넣어줄 수 있다는 사실에 놀랐다.  
기존에는 PriorityQueue를 int 타입 위주로 활용하려고 했었는데, 이를 앎으로써, 더 다양하게 활용해볼 수 있을 것 같다.  
안 그래도 요즘애 프로그래머스 Heap 문제를 풀어보고 있는데, 이를 적극적으로 활용해봐야겠다.

</br>

그리고 풀이는, 안타깝게도 내 수준에서 이해할 수 없는 부분이 있다.  
바로 ListNode 타입의 result와 관련된 로직이 없는데 어떻게 해서 result 안에 결과물이 정렬되어 있냐는 점이다.  
이는 Linked List를 공부해봐야 알 것 같다.  
Linked List를 너무 얕보고 공부를 게을리 넘어가니 이렇게 되었다.  
확실하게 공부하고 짚고 넘어와서 다시 이 문제 풀이를 살펴보도록 하자.
