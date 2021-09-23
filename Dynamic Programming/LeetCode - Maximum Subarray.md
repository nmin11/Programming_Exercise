## **LeetCode > Dynamic Programming > Maximum Subarray**

</br>

[연습 문제 링크](https://leetcode.com/problems/maximum-subarray/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

</br>

## 영어 지문

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.  
A **subarray** is a **contiguous** part of an array.

</br>

## 추가 사항

- 1 <= nums.length <= 10⁵
- -10⁴ <= nums[i] <= 10⁴

</br>

## 문제 요약

정수 배열 nums가 주어질 때, nums의 부분배열 중 합이 가장 큰 부분배열의 합을 리턴하라.  
부분배열은 인접한 요소들이며, 최소 한 개의 요소를 포함한다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=E5r1cQ-vLgM&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        //d[i] → i번째 원소가 마지막 원소인 부분배열의 합 중 최대값
        //ex) d[2] → max(nums[2], nums[1]+nums[2], nums[0]+nums[1]+nums[2])
        int[] d = new int[nums.length];
        d[0] = nums[0];

        //update d[i]
        for (int i = 1; i < nums.length; i++) {
            d[i] = Math.max(d[i-1]+nums[i],
                           nums[i]);
        }
        /*
        직전 index까지의 최대값에서 현재 index의 값을 더해본 값이
        현재 index 값보다 작다면,
        직전 index까지의 최대값은 무용지물이므로,
        현재 index의 값을 그대로 써버린다.
        */

        int max = d[0];
        for (int num : d) {
            if (num > max) max = num;
        }

        return max;
    }
}
```

1차원 배열 `d`에는 각 index를 마지막 값으로 갖는 부분배열의 합 중 최대값을 그대로 담아둔다.  
`d` 배열에서 해당 index가 마지막인 부분배열의 모든 경우의 수를 고려하기 때문에 1차원 배열에서 사실상 모든 부분배열의 경우의 수를 다 고려하게 되는 것이다.  
따라서 이렇게 완성한 `d` 배열의 값 중 최대값을 찾아내기만 하면 된다.

</br>

Dynamic Programming 문제는 보고도 이해가 안가는 경우가 많을 것이다.  
직접 값을 적어보면서 이해하는 과정을 거쳐보도록 하자.
