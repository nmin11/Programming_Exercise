## **LeetCode > Array > Majority Element**

<br>

[연습 문제 링크](https://leetcode.com/problems/majority-element/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

<br>

## 영어 지문

Given an array nums of size n, return the majority element.  
The majority element is the element that appears more than ⌊n / 2⌋ times.  
You may assume that the majority element always exists in the array.

<br>

## 추가 사항

- n == nums.length
- 1 <= n <= 5 \* 10⁴
- -2³¹ <= nums[i] <= 2³¹-1

<br>

## 풀이 방법들

승지니어 님께서 이 문제를 해결할 수 있는 3가지 방법에 대해서 설명해주셨다.

### 1. HashMap 사용

HashMap<Integer, Integer>와 같이 사용하여, 앞쪽에 라벨을, 뒤쪽에 카운트를 저장해준다.  
배열을 한 번 루프하면서 중복되는 각 요소들에 대한 카운트를 매긴다.  
이후에 HashMap을 살펴보면서 어떤 요소가 가장 큰 카운트 값을 가지는지 확인한다.

- 시간 : O(n)
- 공간 : O(n)

<br>

### 2. 이중 반복문

배열의 각 요소마다 등장한 횟수를 체크한다.  
이후 가장 많이 등장한 요소를 리턴한다.

- 시간 : O(n²)
- 공간 : O(1)

### 3. 시간 : O(n) / 공간 : O(1) 로 해결하는 방법

2개의 변수를 선언하고 배열을 한 번 루프하면서, 바로 이전과 같은 요소를 만나면 카운트를 늘려주고, 아니면 깎아주는 방식으로 진행한다.  
이렇게 루프를 진행하고 나면, 다음 둘 중 하나는 반드시 참이 된다.

- 과반수 요소가 존재하지 않음
- 과반수 요소는 기존에 선언해둔 변수

예를들어 [3, 2, 3]이 들어왔을 때 다음과 같이 진행된다.

```java
el = 3 => x = 3, cnt = 1
el = 2 => x = 3, cnt = 0
el = 3 => x = 3, cnt = 1
return 3;
```

그런데 만약 [3, 2]가 들어오면 다음과 같이 진행된다.

```java
el = 3 => x = 3, cnt = 1
el = 2 => x = 3, cnt = 0
return 3;
```

사실 x가 정말 과반수가 맞는지를 체크하기 위해서는 루프를 한 번 더 도는 과정이 필요하지만, 이 문제에서는 항상 과반수가 등장하도록 보장된다고 적혀 있기 때문에 루프를 한 번만 돌아도 되는 것이다.

<br>

## 문제 요약

n만큼의 길이를 가지는 배열 `nums`가 주어진다.  
배열 중에서 과반수 이상 반복되는 요소를 반환하라.  
`nums` 배열에는 항상 과반수 이상으로 등장하는 요소가 있도록 보장된다.

<br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=ZaQsnkKPFOs&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int majorityElement(int[] nums) {
        int x = 0, cnt = 0;
        for (int num : nums) {
            if (cnt == 0) {
                x = num;
                cnt++;
            } else if (x == num) {
                cnt++;
            } else {
                cnt--;
            }
        }
        return x;
    }
}
```
