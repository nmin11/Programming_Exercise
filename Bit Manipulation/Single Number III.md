## **LeetCode > Bit Manipulation > Single Number III**

</br>

[연습 문제 링크](https://leetcode.com/problems/single-number-iii/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given an integer array `nums`, in which exactly two elements appear only once and all the other elements appear exactly twice.  
Find the two elements that appear only once.  
You can return the answer in **any order.**

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

</br>

## 추가 사항

- 2 <= nums.length <= 3 \* 10⁴
- -2³¹ <= nums[i] <= 2³¹ - 1
- Each integer in nums will appear twice, only two integers will appear once.

</br>

## 문제 요약

nums라는 정수 배열이 주어진다.  
이 배열에서 2개의 요소들은 한번씩만 등장하며, 그 외 나머지 요소들은 정확히 두번씩 등장한다.  
한번씩만 등장하는 2개의 요소들을 찾아라.  
정답은 **순서와 상관없이** 리턴해도 된다.

반드시 O(n) 시간 복잡도와 O(1) 공간 복잡도를 갖는 알고리듬을 짜야만 한다.

</br>

## [승지니어 님의 풀이](https://youtu.be/Y_4AXo3EmiU)

```java
class Solution {
    /*
    XOR
    1. 배열에 있는 모든 원소를 XOR
    → 이 값은 결국 한번밖에 등장하지 않는 두 원소 x^y의 값과 같음
    → 왜냐하면 두번씩 등장하는 원소들은 각자 XOR하면서 상쇄되어버리기 때문에
    2. x^y 값에서 적어도 한 bit는 1이어야함
    → 두 숫자는 다를 수 밖에 없는 숫자이기 때문에
    → 그 한 bit의 자리에서 1이 나왔다는 뜻은 그 자리의 값이 서로 다르다는 뜻
    3. 그 한 bit 자리를 기준으로 모든 원소를 두 그룹으로 나눌 수 있음
    → 이 두 그룹에서 유일하게 등장하는 원소가 하나씩 있을 것
    */
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for (int num : nums) xor ^= num;

        int idx = 0;
        for (int i = 0; i < 32; i++) {
            if (((xor >> i) & 1) == 1) {
                idx = i;
                break;
            }
        }

        int xor1 = 0;
        int xor2 = 0;

        for (int num : nums) {
            if (((num >> idx) & 1) == 1) {
                xor1 ^= num;
            } else {
                xor2 ^= num;
            }
        }
        int[] result = new int[2];
        result[0] = xor1;
        result[1] = xor2;

        return result;
    }
}
```

비트 연산 문제는 정말 어려운 것 같다.  
하지만 이 또한 많이 접해보지 않아서 그럴 가능성이 크다.  
승지니어 님은 Algorithm & Data Structure에서는 인기 있는 부류의 문제가 아니기 때문에 자주 등장하지는 않지만, 갑자기 등장하게 되면 당황하게 될 가능성이 크기 때문에 알아두면 좋다고 하셨다.  
결국에 많이 보고 많이 풀어보는 수 밖에 없는 것 같다.
