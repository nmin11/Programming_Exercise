## **LeetCode > Array > Merge Sorted Array**

</br>

[연습 문제 링크](https://leetcode.com/problems/merge-sorted-array/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 문제 요약

nums1과 nums2라는 배열이 오름차순으로 주어지고, 두 숫자 m과 n이 주어진다.  
m과 n은 각각 nums1과 nums2에서의 요소들의 개수를 뜻한다.  
nums1과 nums2를 오름차순으로 정렬된 하나의 배열로 합쳐라.

</br>

최종적으로 정렬된 배열은 리턴할 필요가 없다.  
대신에 nums1 안에 합쳐진 배열을 다시 할당하라.  
이를 위해서 nums1은 m+n의 길이를 가지고 있다.  
m은 합쳐지기 전 기존 요소들을 나타내며, 나머지 n은 0들로 채워져 있다.  
따라서 nums1의 m+n의 뒤쪽의 n에 담겨있는 0들은 무시되어야 한다.  
nums2는 n만큼의 길이를 가지고 있다.

</br>

## 추가 사항

- nums1.length == m + n
- nums2.length == n
- 0 <= m, m <= 200
- 1 <= m + n < = 200
- -10⁹ <= nums1[i], nums2[j] <= 10⁹

</br>

## 힌트 #1

두개의 배열 대신 두개의 요소들로 생각했을 때 이 문제를 쉽게 풀 수 있다.  
개별적인 배열들은 이미 정렬되어 있다.  
우리가 알아야 할 것은 어떻게 그들을 엮이게 하는지에 대한 것이다.  
이 문제에 대해 생각해보고 최상의 해결책에 도달할 수 있겠는가?

</br>

## 힌트 #2

단순히 두개의 배열에서 한번에 하나의 요소를 고려하여 결정하고 그에 따라 진행하면 최적의 솔루션에 도달하게 된다.

</br>

## 첫 풀이 (오답)

이 문제에서는 리턴값을 따로 지정해주지 않고, 제출 시 nums1이 어떻게 변했는지를 감지한다.  
하지만 나는 부끄럽게도, 문제를 제대로 읽어보지 않았으며, answer라는 새로운 배열 변수를 선언해서 이를 해결하고자 하였다.  
당연히 테스트 케이스를 돌려본 결과에서는 기존의 nums1의 원본 배열만 출력이 되어 있었고, 나는 도통 원인을 찾아낼 수가 없었다.  
다른 사람의 풀이를 이용해서라도 이 문제를 적어야겠다고 생각한 뒤 '문제 요약' 부분을 정리하고 있었는데···  
**The final sorted array should not be returned by the function, but instead be stored inside the array nums1.**  
라는 구문이 눈에 띄었다.  
최종적으로 정렬된 배열은 리턴할 필요가 없지만 대신에, 정렬된 배열이 nums1 안에 담겨있어야 한다는 뜻이었다.  
이걸 제대로 읽지를 않아서 20 ~ 30분 가량 삽질했다.  
이러한 부끄러운 기록도 돌이켜 봐야 성장을 하기 때문에 이렇게 기록을 남긴다.

```java
import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int[] answer = new int[m + n];
        int temp = 0;

        for (int i = 0; i < m; i++) {
            answer[i] = nums1[i];
        }
        for (int j = m; j < m + n; j++) {
            answer[j] = nums2[temp];
            System.out.println(temp + " " + nums2[temp]);
            temp++;
        }
        Arrays.sort(answer);
    }
}
```

</br>

## 수정한 풀이

위에서 활용했던 로직 구현 방식을 그대로 활용해서 아래와 같은 코드를 작성했더니 테스트 케이스를 통과할 수 있게 되었다.

```java
import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int temp = 0;

        for (int j = m; j < m + n; j++) {
            nums1[j] = nums2[temp];
            temp++;
        }
        Arrays.sort(nums1);
    }
}
```

</br>

## JavaScript 풀이

JavaScript 풀이는 Java 풀이와 상당히 유사했지만, 지난번에 풀었던 프로그래머스의 K번째 수 문제와 같이, 배열을 sort할 때 화살표 함수를 활용해서 문자열이 아닌 숫자를 비교해서 sorting할 수 있도록 해줘야 했다.

```javascript
var merge = function (nums1, m, nums2, n) {
  let temp = 0;
  for (let i = m; i < m + n; i++) {
    nums1[i] = nums2[temp];
    temp++;
  }
  nums1.sort((a, b) => a - b);
};
```

</br>

## 소감

제발 문제를 꼼꼼히 읽자! :angry:
