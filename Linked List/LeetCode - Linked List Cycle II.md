## **LeetCode > Linked List > Linked List Cycle II**

<br>

[연습 문제 링크](https://leetcode.com/problems/linked-list-cycle-ii/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

<br>

## 영어 지문

Given the `head` of a linked list, return _the node where the cycle begins._  
_If there is no cycle, return_ `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer.  
Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to **(0-indexed).**  
It is `-1` if there is no cycle.  
**Note that** `pos` **is not passed as a parameter.**

**Do not modify** the linked list.

<br>

## 예시

![linked list cycle 1](https://user-images.githubusercontent.com/75058239/146770567-4c161247-0f54-4764-b0c4-5d1e826c47cd.png)

**Input:** head = [3,2,0,-4], pos = 1  
**Output:** tail connects to node index 1  
**Explanation:** There is a cycle in the linked list, where tail connects to the second node.

<br>

![linked list cycle 2](https://user-images.githubusercontent.com/75058239/146770584-70006d23-e009-4526-b2af-e724c93ca890.png)

**Input:** head = [1,2], pos = 0  
**Output:** tail connects to node index 0  
**Explanation:** There is a cycle in the linked list, where tail connects to the first node.

<br>

![linked list cycle 3](https://user-images.githubusercontent.com/75058239/146770596-022e1001-8e0d-412f-a1f2-ff137295adaf.png)

**Input:** root = [1], pos = -1  
**Output:** no cycle  
**Explanation:** There is no cycle in the linked list.

<br>

## 추가 사항

- The number of nodes in the list is in the range `[0, 10⁴]`.
- `-10⁵ <= Node.val <= 10⁵`
- `pos` is `-1` or a **valid index** in the linked-list.

<br>

## 문제 요약

linked-list의 head인 `head`가 주어진다.  
사이클이 시작되는 노드를 반환하라.  
만약 사이클이 없다면 `null`을 반환하라.

몇몇 노드는 `next` 포인터를 따라가면 다시 원래 노드로 돌아올 수 있는 사이클이 있다.  
내부적으로, `pos`가 tail의 `next` 포인터와 연결되는 인덱스이다.  
만약 사이클이 없다면 `-1`이다.  
`pos`는 파라미터로 주어지지 않는다는 점을 명심하라.

linked list를 수정하지 말 것.

<br>

## [승지니어 님의 풀이](https://youtu.be/SPKJz8oPJo4)

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

a : 시작 노드부터 루프의 처음 노드까지 길이
b : 루프 전체의 길이
x : 루프의 처음 노드부터 현재 노드까지의 길이

walker와 runner가 만날 때까지 간 거리
walker : a + x
runner : a + n * b + x

2 * walker = runner
2a + 2x = a + n * b + x
a + x = n * b

→ x 지점과 시작 노드부터 walker와 runner를 전진시키면
루프의 처음 노드에서 만나게 됨
*/

public class Solution {
    public ListNode detectCycle(ListNode head) {
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

        if(runner == null) return null;

        ListNode check = head;

        while(check != walker) {
            check = check.next;
            walker = walker.next;
        }

        return check;
    }
}
```

역시나 풀이는 은근히 단순해보이지만 이해가 되질 않는다.  
walker와 runner를 사용하신 이전 Linked List 문제를 다시 살펴보고, 또 다시 풀어봐야겠다.
