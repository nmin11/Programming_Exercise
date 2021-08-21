## **LeetCode > Backtracking > Permutation**

</br>

[연습 문제 링크](https://leetcode.com/problems/permutations/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given an array nums of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

</br>

## 추가 사항

- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are **unique**.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=wxQmnEKNXAM&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tmp = new ArrayList<>();
        backtrack(nums, result, tmp);
        return result;
    }

    public void backtrack(int[] nums, List<List<Integer>> result, List<Integer> tmp) {
        //base
        if (tmp.size() == nums.length) {
            result.add(new ArrayList<Integer>(tmp));
            return;
        }

        //recursion
        for (int num : nums) {
            if (tmp.contains(num)) continue;
            tmp.add(num);
            backtrack(nums, result, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```

backtracking에 대한 이해를 더하기 위해 승지니어 님의 문제 풀이 영상을 한 개 더 찾아보았다.  
뭔가 추상적으로는 이해가 되는데 재귀가 어떻게 호출되어 가는지 명확하게 그려지지는 않는다.  
직접 호출 과정을 하나씩 적어보면서 더 이해를 해봐야 할 것 같다.
