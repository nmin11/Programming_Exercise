## **LeetCode > Hash Table / Doubly-Linked List > LRU Cache**

<br>

[연습 문제 링크](https://leetcode.com/problems/lru-cache/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

<br>

## 영어 지문

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache.**

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists.<br>Otherwise, add the `key-value` pair to the cache.<br>If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

<br>

## 예시

**Input**

```java
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
```

**Output**

```java
[null, null, null, 1, null, -1, null, -1, 3, 4]
```

**Explanation**

```java
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

<br>

## 추가 사항

- 1 <= capacity <= 3000
- 0 <= key <= 10⁴
- 0 <= value <= 10⁵
- At most 2 \* 10⁵ calls will be made to `get` and `put`.

<br>

## 문제 요약

**LRU(Last Recently Used) cache** 의 제약 조건을 따르는 자료 구조를 디자인하라.

LRUCache 클래스 구현:

- `LRUCache(int capacity)` : 양의 정수 `capacity`를 사이즈로 하여 LRU cache 초기화
- `int get(int key)` : key 값이 있으면 `key의 값` 반환, 없으면 `-1` 반환
- `void put(int key, int value)` : key 값이 이미 존재하는 경우 **key 값 업데이트**<br>key 값이 없으면 **key-value를 cache에 추가**<br>이 작업에서 용량이 capacity를 초과했을 경우 **사용 횟수가 가장 적은 key 제거**

<br>

## [승지니어 님의 풀이](https://youtu.be/WOaQfWqlV7A)

```java
class LRUCache {

    /*
    Doubly-Linked List 컨셉
    Linked List 안에서 임의의 값에 접근해야 함
    → Hash Map을 사용해서 O(1) 시간 복잡도로 접근
    */

    public class CacheItem {
        int key;
        int value;
        CacheItem prev;
        CacheItem next;

        public CacheItem(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    CacheItem head;
    CacheItem tail;
    int capacity;
    Map<Integer, CacheItem> map;

    public LRUCache(int capacity) {
        head = null;
        tail = null;
        this.capacity = capacity;
        map = new HashMap<>();
    }

    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        } else {
            CacheItem cur = map.get(key);

            if (cur != head) {
                if (cur == tail) {
                    //move tail to one in front
                    tail = tail.prev;
                }

                //move cur to head
                if (cur.prev != null) {
                    cur.prev.next = cur.next;
                }
                if (cur.next != null) {
                    cur.next.prev = cur.prev;
                }
                cur.next = head;
                head.prev = cur;
                cur.prev = null;
                head = cur;
            }

            return cur.value;
        }
    }

    public void put(int key, int value) {
        if (get(key) == -1) {
            //insert to head
            CacheItem cur = new CacheItem(key, value);

            if (head == null) {
                head = cur;
                tail = cur;
            } else {
                cur.next = head;
                head.prev = cur;
                head = cur;
            }

            map.put(key, cur);

            if (map.size() > capacity) {
                //evict tail
                map.remove(tail.key);
                tail.prev.next = null;
                tail = tail.prev;
            }
        } else {
            //update
            map.get(key).value = value;
        }
    }

}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

Database에 자주 등장하는 cache라는 용어도 그렇고, LRU도 꽤나 많이 등장하는 용어이다보니, 이러한 요소들이 내부적으로 어떤 동작을 하는지 짐작해보게 하는 좋은 문제이다.  
이러한 cache 관련 로직을 또한 O(1) 시간 복잡도로 구현해야 하기 때문에 이 문제는 꽤나 까다롭지만 역시나 효율적인 작동 방식을 고려하게 하는 좋은 포인트였다.  
이번에는 승지니어 님의 영상을 보고 풀이를 참조했지만, 나중에 꼭 초기화해서 다시 풀어보고 싶은 문제였다.  
그만큼 재미 있는 문제였고, O(1) 시간 복잡도에 관한 로직을 고민해보기에 좋은 문제라고 생각한다.  
더불어서, GeeksforGeeks 사이트에서 LRU 관련 포스팅들을 읽어보고, 추가적으로 정리해보는 시간을 가져야만 하겠다.
