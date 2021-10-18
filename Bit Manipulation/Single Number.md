## **LeetCode > Bit Manipulation > Single Number**

</br>

[연습 문제 링크](https://leetcode.com/problems/single-number/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

</br>

## 영어 지문

Given a **non-empty** array of integers nums, every element appears twice except for one.  
Find that single one.  
You must implement a solution with a linear runtime complexity and use only constant extra space.

</br>

## 추가 사항

- 1 <= nums.length <= 3 \* 10⁴
- -3 \* 10⁴ <= nums[i] <= 3 \* 10⁴
- Each element in the array appears twice except for one element which appears only once.

</br>

## 문제 요약

비어있지 않은 정수들의 배열이 주어진다.  
모든 요소는 오직 하나의 요소만 제외하고는 모두 두번씩 반복된다.  
반복되지 않는 단 하나의 요소를 찾아라.  
또한, 선형적인 시간 복잡도와 상수의 공간 복잡도를 가진 해결책을 제시해야 한다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=3J_UlbwUfc0&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) result ^= num;
        return result;
    }
}
```

비트연산(XOR)에 대한 가장 기본적인 문제라고 한다.  
하지만 이 비트연산에 대한 이해도가 전무하다보니 이해가 잘 안되었다.  
반드시 추가적인 공부를 진행해서 TIL에 올릴 수 있도록 해야겠다.
