## **LeetCode > Linked List > Linked List Cycle**

<br>

[연습 문제 링크](https://leetcode.com/problems/linked-list-cycle/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

<br>

## 영어 지문

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer.  
Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to.  
**Note that** `pos` **is not passed as a parameter.**

Return `true` _if there is a cycle in the linked list._  
Otherwise, return `false`.

<br>

## 예시

(이미지 첨부 1번)

**Input:** head = [3,2,0,-4], pos = 1  
**Output:** true  
**Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

<br>

(이미지 첨부 2번)

**Input:** head = [1,2], pos = 0  
**Output:** true  
**Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

<br>

(이미지 첨부 3번)

**Input:** root = [1], pos = -1  
**Output:** false
**Explanation:** There is no cycle in the linked list.

<br>

## 추가 사항

- The number of nodes in the list is in the range `[0, 10⁴]`.
- `-10⁵ <= Node.val <= 10⁵`
- `pos` is `-1` or a **valid index** in the linked-list.

<br>

## 문제 요약

linked-list의 head인 `head`가 주어진다.

몇몇 노드는 `next` 포인터를 따라가면 다시 원래 노드로 돌아올 수 있는 사이클이 있다.  
내부적으로, `pos`가 tail의 `next` 포인터와 연결되는 인덱스이다.  
여기서 `pos`는 직접적으로 주어지지 않는다는 점을 명심하라.

linked-list에 사이클이 있으면 `true`를, 그렇지 않다면 `false`를 반환하라.

<br>

## [승지니어 님의 풀이](https://youtu.be/3dR3UtADdBQ)

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

/*
walker : 한번에 한칸씩
runner : 한번에 두칸씩
→ 사이클이 있으면 둘은 언젠가 만남
→ 사이클이 없으면 runner가 먼저 null에 닿음

시간복잡도 O(n)
공간복잡도 O(1)
*/

public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode walker = head;
        ListNode runner = head;

        while(runner != null) {
            runner = runner.next;

            if(runner != null) {
                runner = runner.next;
                walker = walker.next;

                if(runner == walker) break;
            } else break;
        }

        if(runner == null) return false;
        else return true;
    }
}
```

이번 문제는 승지니어 님의 영상을 보기 전에 먼저 풀어보려고 시도했다.  
하지만 부끄럽게도 문제가 이해가 되질 않았다.  
(심지어 파파고 번역을 돌려보고도 뭔 말인지 한참을 쳐다봤고, 승지니어 님 영상을 보고나서도 사실 이해가 명쾌하게 되지 않았다)

그래도 정리하면서 들여다보니 핵심은 이런 느낌인 것 같다.  
우선 `head`가 예시에서 배열 형태로 보여지는 것으로 보아, 그 배열의 인덱스 순서대로 link가 연결된 linked-list가 주어지고, 이 linked-list의 tail, 즉, 맨 끝 부분에 도달했을 때 우리는 모르는 메소드 내부의 `pos`라는 별도의 값을 인덱스로 갖는 요소로 돌아간다는 뜻인 것 같다.  
그리고 이렇게 돌아간 인덱스의 값이 이전에 `head`부터 `tail`까지 도달하면서 이미 거쳐간 값인지를 검증하라는 느낌으로 받아들였다.

사실 이렇게 문제에 대한 이해도가 많이 부족했던 만큼 풀이에 대한 이해가 잘 안되었다.  
사실 풀이를 상당히 단순하게, 이해하기 쉽게 잘 풀어주신 것 같지만, 이는 추후 linked-list에 대해 학습하고 다시 알아봐야 할 것 같다.  
이해를 못한 만큼 이번 문제는 다음 기회에 꼭 초기화를 해서 다시 풀어보도록 하자.
