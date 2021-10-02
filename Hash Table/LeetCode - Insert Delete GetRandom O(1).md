## **LeetCode > Hash Table > Insert Delete GetRandom O(1)**

</br>

[연습 문제 링크](https://leetcode.com/problems/insert-delete-getrandom-o1/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Implement the RandomizedSet class:

- RandomizedSet() Initializes the RandomizedSet object.
- bool insert(int val) Inserts an item val into the set if not present.  
  Returns true if the item was not present, false otherwise.
- bool remove(int val) Removes an item val from the set if present.  
  Returns true if the item was present, false otherwise.
- int getRandom() Returns a random element from the current set of elements  
  (it's guaranteed that at least one element exists when this method is called).  
   Each element must have the same probability of being returned.

You must implement the functions of the class such that each function works in **average** O(1) time complexity.

</br>

## 추가 사항

- -2³¹ <= val <= 2³¹ - 1
- At most 2 \* 10⁵ calls will be made to insert, remove, and getRandom.
- -There will be **at least one** element in the data structure when getRandom is called.

</br>

## 문제 요약

RandomizedSet 클래스를 다음과 같이 구현하라.

- RandomizedSet()은 RandomizedSet 객체의 초기화 작업
- bool insert(int val)는 val 값을 이미 갖고 있지 않을 때 해당 값을 삽입한다.  
  val 값을 갖고 있지 않으면 true, 갖고 있으면 false를 반환한다.
- bool remove(int val)는 val 값을 찾아서 삭제한다.  
  val 값을 갖고 있으면 true, 갖고 있지 않으면 false를 반환한다.
- int getRandom()은 데이터에서 랜덤하게 요소를 꺼내온다.  
  (이 메소드가 호출될 때, 최소 한 개의 요소는 남아있음을 보장한다.)  
  모든 요소들은 동일하게 리턴될 수 있는 가능성을 가진다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=dei_SHqRIZ8&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class RandomizedSet {

    //key : el, val : idx
    Map<Integer, Integer> map;
    ArrayList<Integer> list;
    //# of valid elements in the list
    int size;
    Random r = new Random();

    public RandomizedSet() {
        map = new HashMap<>();
        list = new ArrayList<>();
        size = 0;
    }

    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        map.put(val, size++);
        list.add(val);

        return true;
    }

    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        int idx = map.get(val);
        map.remove(val);
        if (idx != size-1) {
            int swap = list.get(size-1);
            list.set(idx, swap);
            map.put(swap, idx);
        }
        list.remove(--size);

        return true;
    }

    public int getRandom() {
        int idx = r.nextInt(size);
        return list.get(idx);
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

O(1) 시간복잡도로 문제를 해결해야 하기 때문에 좀 까다롭다.  
일단 Hash Map을 사용하면 특정 값을 가져오거나 삭제하는 작업 정도는 간단하게 해결할 수 있다.  
하지만 getRandom()의 경우에는 랜덤하게 값을 가져오기 때문에, 결국 Hash Map을 요소들의 개수만큼 순회해야 한다.  
따라서 Hash Map만 가지고서는 O(1) 시간복잡도로 해결할 수 없다.  
이를 보조하기 위한 자료구조가 ArrayList이다.  
Random 클래스를 활용해서 size 안에 랜덤 숫자를 얻고, ArrayList로 해당 랜덤 숫자를 뽑아오는 작업은 O(1) 시간복잡도로 해결 가능하다.

</br>

remove 메소드의 로직이 조금 헷갈렸는데, 해당 로직은 다음과 같이 작동한다.

```
list : 1, 2, 3, 4 => size : 4
remove 2
list : 1, 4, 3 => size : 3
```

어짜피 RandomizedSet은 랜덤으로 자료를 가져오기 위한 목표를 가지고 있으니 순서가 섞이는 것에 대해 염려할 필요가 없는 것이다.  
그리고 Hash Map에서도 이전 val 값을 지우고 다시 list에 지정된 idx 값으로 인덱스를 지정해주면 된다.
