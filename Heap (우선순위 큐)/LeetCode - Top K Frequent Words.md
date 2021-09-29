## **LeetCode > Heap (Priority Queue) > Top K Frequent Words**

</br>

[연습 문제 링크](https://leetcode.com/problems/top-k-frequent-words/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given an array of strings words and an integer k, return the k most frequent strings.  
Return the answer **sorted** by **the frequency** from highest to lowest.  
Sort the words with the same frequency by their **lexicographical order**.

</br>

## 추가 사항

- 1 <= words.length <= 500
- 1 <= words[i] <= 10
- words[i] consists of lowercase English letters.
- k is in the range [1, The number of **unique** words[i]]

</br>

## 문제 요약

문자열들을 담은 배열과 정수 k가 주어진다.  
k개의 가장 많이 반복되는 문자열들을 리턴하라.  
리턴값은 반복 횟수를 기준으로 내림차순 정렬해야 한다.  
만약 반복 횟수가 동일할 경우, 알파벳 사전 순서대로 정렬하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=8XhXg98E1Gg&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public class WordCnt {
        String word;
        int cnt;
        public WordCnt(String word) {
            this.word = word;
            this.cnt = 1;
        }
    }

    public List<String> topKFrequent(String[] words, int k) {
        Map<String, WordCnt> map = new HashMap<>();
        for (String word : words) {
            if (map.containsKey(word)) {
                map.get(word).cnt++;
            } else {
                map.put(word, new WordCnt(word));
            }
        }

        //min heap, k개 : 항상 top k frequent element를 오름차순으로 가지고 있음
        PriorityQueue<WordCnt> pq = new PriorityQueue<>(k, (a,b) -> a.cnt - b.cnt != 0 ?
                                                        a.cnt - b.cnt : b.word.compareTo(a.word));
        for (WordCnt wordCnt : map.values()) {
            pq.offer(wordCnt);
            if (pq.size() > k) pq.poll();
        }

        List<String> result = new ArrayList<>();
        while (!pq.isEmpty()) {
            result.add(0, pq.poll().word);
        }

        return result;
    }
}
```
