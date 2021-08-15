## **LeetCode > Heap (Priority Queue) > Kth Largest Element in an Array**

</br>

[연습 문제 링크](https://leetcode.com/problems/kth-largest-element-in-an-array/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Medium

</br>

## 영어 지문

Given an integer array nums and an integer k, return the kth largest element in the array.  
Note that it is the kth largest element in the sorted order, not the kth distinct element.

</br>

## 추가 사항

- 1 <= k <= nums.length <= 10⁴
- -10⁴ <= nums[i] <= 10⁴

</br>

## 문제 요약

정수로 된 배열 nums와 int 타입의 k가 인자로 주어진다.  
주어진 배열에서 k번째로 큰 요소를 리턴하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=ifGUwB_PCt4&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    /*
    우선순위 큐
    오름차순 정렬이 기본
    offer : 3 2 1 5 4 -> poll : 1 2 3 4 5
    시간복잡도 offer/poll O(log n)
    */

    /*
    문제풀이 전략
    큐에는 k개의 원소를 보관
    확인한 원소 중 가장 큰 k개
    큐의 맨 앞에는 k개 중 가장 작은 것이 있음
    */

    PriorityQueue<Integer> pq = new PriorityQueue<>();
    public int findKthLargest(int[] nums, int k) {
        for (int num : nums) {
            if (pq.size() < k) {
                pq.offer(num);
            } else {
                if (num > pq.peek()) {
                    pq.poll();
                    pq.offer(num);
                }
            }
        }
        return pq.peek();
    }
}
```

Java에서 제공해주는 Priority Queue라는 친구에 대해서 공부해봤다.  
이 친구는 pq.offer를 해주기만 하면 자신이 갖고 있는 요소들을 알아서 정리해준다고 한다.  
그 밖에 나머지 메소드의 활용 등은 일반 Queue와 흡사했다.

</br>

문제 풀이 방식은 우선 pq에 k개까지의 요소들을 담고, 그 다음 요소들에 대해서는 큐에 있는 숫자보다 큰 값들에 한해서 큐에 넣어줌과 동시에 FIFO 작업을 진행해주는 방식으로 진행되었다.  
이렇게 하면 pq에는 알아서 k개의 숫자 만큼만 있게 되고, pq는 알아서 정렬이 되기 때문에 pq의 맨 앞의 값을 가져오면 그 값이 알아서 k번째 값이 되는 놀라운 방식이었다.
