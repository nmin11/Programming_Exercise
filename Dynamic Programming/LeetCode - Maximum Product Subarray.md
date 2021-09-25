## **LeetCode > Dynamic Programming > Maximum Product Subarray**

</br>

[연습 문제 링크](https://leetcode.com/problems/maximum-product-subarray/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.  
It is **guaranteed** that the answer will fit in a **32-bit** integer.  
A **subarray** is a contiguous subsequence of the array.

</br>

## 추가 사항

- 1 <= nums.length <= 2 \* 10⁴
- -10 <= nums[i] <= 10

</br>

## 문제 요약

정수 배열이 주어진다.  
배열 안에서 최대의 곱을 가지는 인접한 부분배열을 리턴하라.  
정답이 32bit 범위 이내의 정수라는 것이 보장된다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=MGwd30-ZM6o&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int maxProduct(int[] nums) {
        int[][] d = new int[nums.length][2];
        /*
        d[i][0] → 0~i 가장 큰 값
        d[i][1] → 0~i 가장 작은 값
        */
        d[0][0] = nums[0];
        d[0][1] = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int c = nums[i];
            d[i][0] = Math.max(c, Math.max(c * d[i-1][0],
                                          c * d[i-1][1]));
            d[i][1] = Math.min(c, Math.min(c * d[i-1][0],
                                          c * d[i-1][1]));
        }

        int max = d[0][0];
        for (int i = 0; i < nums.length; i++) {
            if (d[i][0] > max) max = d[i][0];
        }
        return max;
    }
}
```

이번 문제는 0이 곱해지거나 음수가 곱해질 수 있는 경우의 수 때문에 이에 대해 고려해봐야 한다.  
승지니어 님은 메모이제이션 배열을 2차원 배열로 사용해서, 최대값과 최소값을 각각 저장해두었다.  
음수인 최소값에 음수가 곱해져서 최대값이 될 수도 있는 경우의 수를 고려하신 것이다.
