## **LeetCode > Stack > Min Stack**

</br>

[연습 문제 링크](https://leetcode.com/problems/min-stack/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Easy

</br>

## 영어 지문

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

</br>

Implement the MinStack class:

- **MinStack()** initializes the stack object.
- **void push(val)** pushes the element val onto the stack.
- **void pop()** removes the element on the top of the stack.
- **int top()** gets the top element of the stack.
- **int getMin()** retrieves the minimum element in the stack.

</br>

## 추가 사항

- -2³¹ <= val <= 2³¹ - 1
- Methods pop, top and getMin operations will always be called on **non-empty** stacks.
- At most 3 \* 10⁴ calls will be made to push, pop, top, and getMin.

</br>

## 문제 요약

push, pop, top, 그리고 상수 시간 복잡도로 최소값을 검색하는 getMin을 구현하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=5MnhCfeLyhg&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class MinStack {
    /*
    pop을 통해 요소를 뺐을 때,
    이전의 최소값은 기억되고 있다.
    push되는 각 상황마다 최소값을 기억하면 된다.
    */

    class Node {
        int val, min;
        Node(int val, int min) {
            this.val = val;
            this.min = min;
        }
    }

    Stack<Node> s = new Stack<>();

    /** initialize your data structure here. */
    public MinStack() {

    }

    public void push(int val) {
        Node node = null;
        if (s.isEmpty()) {
            node = new Node(val, val);
        } else {
            node = new Node(val, val < s.peek().min ? val : s.peek().min);
        }
        s.push(node);
    }

    public void pop() {
        s.pop();
    }

    public int top() {
        return s.peek().val;
    }

    public int getMin() {
        return s.peek().min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

이 문제의 핵심이 되는 부분은 상수 시간 복잡도로 최소값을 구하는 부분이다.  
이를 위해 Node 클래스를 따로 구현하여 Stack의 각 요소마다 자신의 값과 현재 최소값을 기억해두도록 했다.  
이를 위해 가장 중요하게 사용되는 메소드가 push이다.  
push를 할 때 마다 현재 최소값과 삽입하려는 값을 비교하여 최소값을 계속 갱신해주는 것이다.

</br>

## 여담

영상을 보기 전에 문제를 먼저 확인해보고는, '이 정도는 어떻게 풀어볼 수 있지 않을까?' 하는 생각이 들어서 직접 풀어보려는 시도를 했었다.  
하지만 안타깝게도 감을 못 잡고 10분 정도 멀뚱히 문제를 보고 있는 자신을 발견하고는, 그냥 영상을 통해 공부를 진행했다.  
너무 자존심 상할 것 없이, 문제를 풀어나가는 원리 및 방법에 대해 충분히 학습하고자 한다.
