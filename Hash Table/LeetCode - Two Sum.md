## **LeetCode > Array / Hash Table > Two Sum**

</br>

[연습 문제 링크](https://leetcode.com/problems/two-sum/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 영어 지문

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.  
You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

## 추가 사항

- 2 <= nums.length <= 10⁴
- -10⁹ <= nums[i] <= 10⁹
- -10⁹ <= target <= 10⁹
- **Only one valid answer exists**

</br>

## 문제 요약

숫자들로 이루어진 배열과 숫자로 된 타겟이 주어졌을 때, 배열 안에 숫자 두개를 더해서 타겟이 될 수 있는 배열 안의 2개의 숫자들의 인덱스들을 배열에 담아서 리턴해라.  
배열 안에서 숫자 2개를 더해서 타겟이 되는 쌍이 딱 한 쌍 밖에 없다고 가정해도 좋다.  
그리고 같은 요소를 두 번 사용할 수는 없다.

</br>

## 문제를 풀기 전 알아둬야 할 점

이 문제 또한 [승지니어](https://www.youtube.com/watch?v=ly-zKS3ubYo&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer) 님의 영상을 참고하여 같이 풀어보게 되었다.  
문제 풀이 전, 기술면접에 있어서 아주 중요하게 참고해둬야 할 점이 있어서 이렇게 옮겨 적게 되었다.

</br>

기술면접에서는 자신이 설계를 먼저 하고나서 구현을 해야한다.  
즉, 아이디어를 먼저 제시하고, 그 다음이 문제 풀이라는 것이다.  
따라서, 시간복잡도와 공간복잡도를 먼저 생각해봐야 한다.  
이 문제의 경우, 시간복잡도와 공간복잡도를 따져보았을 때, 2가지 대안이 존재한다.

</br>

### 대안 1. brute-force

모든 조합을 시도해본다.  
이는 **n \* (n-1) / 2** 라고 볼 수 있으며 2중 루프를 돌게 된다.

- 시간 : O(n²)
- 공간 : O(1)

</br>

### 대안 2. Hash Map 사용

루프 1개들 돌면서 이미 봤던 값을 Hash Map에 넣는다.

- 시간 : O(n)
- 공간 : O(n)

</br>

### 선택해야 될 대안

기술면접에서는 보통 시간복잡도를 우선적으로 고려한다.  
그렇다고 해서 대안2의 방법만 알아둘 게 아니라, 대안1, 대안2를 모두 충분히 숙지한다면 기술면접에서 말할 수 있는 소재가 더더욱 늘어날 것이다.

</br>

## 대안 1. brute-force

```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                int[] temp = new int[2];
                temp[0] = i;
                temp[1] = j;
                return temp;
            }
        }
    }
    return null;
}
```

사실, 참 직관적이고 이해하기도 쉽다.  
하지만 기술면접을 위해서는 꼭 대안2의 방법을 숙지해둬야만 한다.

</br>

## 대안 2. Hash Map

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>(); //key=el, val=idx

    for (int i = 0; i < nums.length; i++) {
        int cur = nums[i];
        if (map.containsKey(target - cur)) {
            int[] temp = new int[2];
            temp[0] = map.get(target - cur);
            temp[1] = i;
            return temp;
        } else {
            map.put(cur, i);
        }
    }
    return null;
}
```

nums 배열을 순회하는 반복문 안에서 Map을 활용하여, target에서 nums의 요소를 뺀 값이 이미 존재하는지 확인한다.  
존재한다면 해당 값의 인덱스를 찾아서, 해당 값의 인덱스와 nums의 요소의 인덱스를 배열에 담아서 반환한다.  
존재하지 않는다면 nums의 요소와 인덱스를 Map에 담아둔다.  
이 풀이는 대안 1에 비해서 테스트를 빨리 통과하는 모습을 확인할 수 있었다.

</br>

## 소감

냉정하게 봤을 때 나는 대안2와 같은 풀이가 눈에 익지 않다.  
아직 그만큼 익숙하지 않다는 뜻이다.  
좋은 풀이를 보고 공부하는 것도 좋지만, 직접 활용해서 더 많은 문제들을 풀어봐야겠다.
