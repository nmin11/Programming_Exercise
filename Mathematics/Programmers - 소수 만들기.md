## **Programmers > Summer/Winter Coding(~2018) > 소수 만들기**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12977)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구한다.  
숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return하시오.

</br>

## 추가 사항

- 3 <= nums.length <= 50
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자는 없음

</br>

## 나의 풀이 (오답)

```java
import java.util.*;

class Solution {
    public int solution(int[] nums) {
        List<Integer> sums = new ArrayList<Integer>();
        int sum;

        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums.length; j++) {
                for (int k = 0; k < nums.length; k++) {
                    if (i != j && i != k && j != k && sums.contains(nums[i] + nums[j] + nums[k]) == false) {
                        sum = nums[i] + nums[j] + nums[k];
                        boolean isPrime = true;
                        for (int l = 2; l < sum; l++) {
                            if (sum % l == 0) {
                                isPrime = false;
                                break;
                            }
                        }
                        if (isPrime) {
                            sums.add(sum);
                        }
                    }
                }
            }
        }

        return sums.size();
    }
}
```

주어진 배열을 3중 for문으로 돌리면서 i와 j와 k의 값이 서로 다른 조건을 찾는다.  
이후 기존에 준비해 둔 소수들을 담을 ArrayList에 세 인덱스에 해당하는 값들을 더한 값이 없는 조건에 한해 소수인지 여부를 구하는 연산을 한다.  
이렇게 소수들을 차례차례 담고, 마지막에 ArrayList의 size를 그대로 반환하려고 했다.  
'코드 실행' 탭을 눌렀더니 2가지 테스트 케이스를 통과했다.  
하지만 '제출 후 채점' 탭을 눌렀더니 26가지 테스트 케이스에서 단 6가지의 테스트 케이스만 통과했다. :disappointed_relieved:  
이후 생각해봐도 답이 나오지 않아서 어쩔 수 없이 다른 사람의 풀이를 찾아보았다.

</br>

## 다른 사람의 풀이

```java
class Solution {
   public int solution(int[] nums) {
      int answer = 0;
      boolean chk = false;

      for (int i = 0; i < nums.length; i++) {
         for (int j = i + 1; j < nums.length; j++) {
            for (int k = j + 1; k < nums.length; k++) {
               int num = nums[i] + nums[j] + nums[k]; //값을 담아
               if (num >= 2) //경우의 수를 찾아서
                  chk = sosu(num);
               if (chk == true) //소수가 맞을 경우
                  answer++;

            }
         }

      }
      return answer;
   }

   public boolean sosu(int num) {
      boolean check = true;
      if(num==2) { //소수일때
         return check;

      }
      for(int i=2; i<num; i++) { //소수가 아닐때
         if(num%i ==0) {
            check = false;
            break;
         }
      }
      return check;
   }
}
```

ArrayList를 쓰지도 않았다.  
그리고 내가 한 가지 간과했던 점, i와 j와 k의 모든 경우의 수를 구할 필요가 없었다는 점이다.  
소수를 구하는 함수를 따로 빼낸 것도 기발했다.
