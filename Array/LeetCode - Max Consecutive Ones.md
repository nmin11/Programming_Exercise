## **LeetCode > Array > Max Consecutive Ones**

</br>

[연습 문제 링크](https://leetcode.com/problems/max-consecutive-ones/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 문제 요약

이진법(0, 1)의 숫자만을 요소로 갖는 nums라는 배열이 있다.  
배열 안에서 1이 연속되는 횟수의 최대값을 반환해라.

</br>

## 추가 사항

- 1 <= nums.length <= 10⁵
- nums[i]는 0 아니면 1

</br>

## 힌트

창(window)에 관한 두 가지 것에 대해 생각해봐야 한다.  
하나는 창의 시작점에 관한 것이다. 어떻게 1이 연속되는 부분의 시작점을 감지할 수 있겠는가?  
다음은 창의 마지막 부분을 감지하는 것이다. 어떻게 존재하는 창의 마지막 포인트를 감지할 수 있겠는가?  
이 두 가지를 생각해냈다면, 연속된 창을 감지할 수 있게 된다.  
그 다음으로 남은 것은 가장 긴 창을 찾아서 그 사이즈를 반환하는 일이다.

</br>

## 다른 사람의 풀이

처음에 이 문제를 딱 봤을 때 정말 간단한 문제겠거니, 했는데 안타깝게도 풀어나갈 수 있는 실마리를 찾지 못했다.  
30분 가량을 문제에 제대로 손도 대보지 못하고 있다가 도저히 안되겠다 싶어서 Discuss 탭에서 다른 사람의 풀이를 참고했다.  
원래 이 Programming_Exercise라는 Repository에는 내가 제대로 풀어냈으며 이해가 잘 된 상태의 문제들을 정리하려고 하였으나, 이 문제는 상당히 단순한 듯 보이는 문제임에도 내가 잘 풀어내지 못했으니, 원리를 제대로 이해해보고자 하는 마음에 이렇게 기록을 남기게 되었다.

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int maximum = -1, count = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 1){
                count++;
            }else{
                if(count > maximum){
                    maximum = count;
                }
                count = 0;
            }
        }
        if(count > maximum){
            maximum = count;
        }
        return maximum;
    }
}
```

문제가 단순했듯, 풀이도 단순했다.  
처음에는 1을 만날 때마다 count++을 해준다.  
0을 만났을 때에는 그렇게 ++된 count 값이 기존의 maximum과 비교해서 더 클 때 count의 값을 maximum에 대입해주고, count를 0으로 초기화한다.  
for문 바깥의 if문은 맨 마지막 인덱스의 값이 0이 아니라 1일 때 마찬가지로 count 값과 maximum 값을 비교하여 count 값이 더 크면 maximum에 대입해주기 위해 존재한다.

</br>

## 소감

자괴감이 많이 들었던 문제이다.  
나는 아직도 한참 부족한 게 맞지만, 요즘에 프로그래머스의 Level 문제들을 풀어나갔다 보니 이 문제를 처음 접했을 때, '이 정도 문제는 풀 수 있지 않을까?' 하는 생각에 이 문제를 가볍게 보았다.  
하지만 그런 내 자만심이 무참히 깨졌다.  
그만큼 나는 지금 코딩 테스트 문제 풀이에 정말 최악일 정도로 실력이 낮다.  
더 많은 문제를 깊이 고민해보면서 풀어야겠다.  
스스로 생각하며 문제를 풀어나갈 수 있도록 다른 사람의 풀이를 쳐다보지 않도록 더 자제해야겠다.
