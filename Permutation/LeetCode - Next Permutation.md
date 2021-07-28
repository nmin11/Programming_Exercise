## **LeetCode > Array / Two Pointers > Valid Parentheses**

</br>

[연습 문제 링크](https://leetcode.com/problems/valid-parentheses/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Medium

</br>

## 영어 지문

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

</br>

## 문제 요약

사전식 순서에 따라 바로 다음으로 큰 수에 해당하는 **다음 순열**이 오도록 구현하라.  
그러한 배열이 불가능한 경우, 가능한 가장 낮은 순서(즉, 오름차순으로 정렬)로 재배열해야 한다.  
일정한 추가 메모리만 사용하여 원래 입력을 반환해야 한다.

</br>

## 추가 사항

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 100

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=mbOl9qPedDo&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    /*
    1 3(a) 5 4 4(b)
    => 1 4 3 4 5

    5 4 3 2 1 인 경우도 생각해서 풀어야 함
    */
    public void nextPermutation(int[] nums) {
        //뒤에서부터 탐색하면서 오름차순이 깨지는 인덱스 확인(a)
        int a = nums.length - 2;
        while (a >= 0 && nums[a] >= nums[a + 1]) a--;

        if (a != -1) {
            //다시 뒤에서부터 탐색하면서 a보다 큰 첫번째 인덱스를 확인(b)
            int b = nums.length - 1;
            while (nums[a] >= nums[b]) b--;
            //a랑 b를 스왑
            swap(nums, a, b);
        }

        //a + 1에서부터 끝까지를 오름차순으로 정렬
        int start = a + 1;
        int end = nums.length - 1;
        while (start < end) {
            swap(nums, start++, end--);
        }
    }

    public void swap(int[] nums, int a, int b) {
        int tmp = nums[a];
        nums[a] = nums[b];
        nums[b] = tmp;
    }
}

```

승지니어 님도 본래 문제를 외워서 푸는 방식을 권하지 않지만, 이 문제 만큼은 왜 이런걸 풀어야 하는지 모르겠다고 하시면서, 정 이해가 안되면 외워도 된다고 했던 풀이이다.  
다만 기술 면접에서 꽤나 심심찮게 등장하는 문제인 만큼 어느 정도의 설명을 곁들일 수 있어야만 하겠다.
