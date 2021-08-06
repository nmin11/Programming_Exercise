## **LeetCode > Array / Binary Search > Search in Rotated Sorted Array**

</br>

[연습 문제 링크](https://leetcode.com/problems/search-in-rotated-sorted-array/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Medium

</br>

## 영어 지문

There is an integer array nums sorted in ascending order (with **distinct** values).  
Prior to being passed to your function, nums is **rotated** at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (**0-indexed**).  
For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].  
Given the array nums **after** the rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.  
You must write an algorithm with O(log n) runtime complexity.

</br>

## 추가 사항

- 1 <= nums.length <= 5000
- -10⁴ <= nums[i] <= 10⁴
- All values of nums are **unique**.
- nums is guaranteed to be rotated at some pivot.
- -10⁴ <= target <= 10⁴

</br>

## 문제 요약

값이 구별되며, 오름차순으로 정렬된 정수 배열이 있다.  
배열 nums는 함수에 전달되기 전에, pivot을 기준으로 왼쪽과 오른쪽의 배열이 서로 바뀐다.  
회전하여 변경된 배열의 요소 중 target과 일치하는 것이 있으면 해당 요소의 인덱스를 리턴하고, 없으면 -1을 리턴하라.  
반드시 O(log n) 복잡도를 가진 Algorithm을 작성해야 한다.

</br>

## 풀이

```java
public int search(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {
        int middle = (left + right) / 2;
        if (nums[middle] == target) return middle;

        if (nums[left] <= nums[middle]) {
            if (nums[left] <= target && nums[middle] > target) {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        } else {
            if (nums[middle] < target && nums[right] >= target) {
                left = middle + 1;
            } else {
                right = middle - 1;
            }
        }
    }
    return -1;
}
```

왼쪽 값이 middle 값보다 작거나 같은 경우, target 값을 비교해서 middle의 왼쪽 편에 있는 배열이 정렬되어 있는지 확인한다.  
조건에 맞는다면, right 값을 middle 값으로 조정하고, 맞지 않다면 left 값을 middle 값으로 조정한다.  
반대의 경우에는 마찬가지로 오른쪽이 정렬되어 있는지 확인하면서 left와 right를 조정한다.
