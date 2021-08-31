## **Programmers > 스택/큐 > 기능개발**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42587)

</br>

📚 내가 사용한 프로그래밍 언어 : JavaScript  
🎢 난이도 : Level 2

</br>

## 문제 요약

중요도가 높은 문서를 먼저 인쇄하는 프린터가 있다.  
이 프린터는 아래와 같은 방식으로 인쇄 작업을 수행한다.

1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼낸다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣는다.
3. J보다 중요도가 높은 문서가 없을 경우 J를 인쇄한다.

예를 들어, 4개의 문서 `A, B, C, D`가 순서대로 인쇄 대기목록에 있고 중요도가 `2, 1, 3, 2`라면 `C - D - A - B` 순으로 인쇄하게 된다.  
개발자 L은 본인이 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶다.  
현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 L이 인쇄를 요청한 문서가 대기목록의 어떤 위치에 있는지 알려주는 location이 매개변수로 주어질 때, L이 인쇄를 요청한 문서가 몇 번째로 인쇄되는지를 리턴하라.

</br>

## 추가 사항

- 1 <= priorities.length <= 100
- 1 <= priorities[i] <= 9
- location은 0부터 세어나가기 때문에 priorities에서 index 값으로 적용해서 찾아낼 수 있다.

</br>

## 내 풀이 (JavaScript)

```javascript
function solution(priorities, location) {
  const handleMax = (arr) => {
    let max = 0;
    for (let el of arr) {
      if (el[0] > max) max = el[0];
    }

    while (queue[0][0] !== max) {
      let el = queue.shift();
      queue.push(el);
    }
  };

  let queue = [];
  for (let i = 0; i < priorities.length; i++) {
    queue.push([priorities[i], i]);
  }

  handleMax(queue);

  let count = 0;
  while (queue.length > 0) {
    count++;
    if (queue[0][1] === location) {
      return count;
    } else {
      queue.shift();
      handleMax(queue);
    }
  }
}
```

가장 아쉬운 점은 Java로 해결할 수 있는 뾰족한 수를 찾지 못해서 JavaScript로 우회해서 풀었다는 점이다.  
Queue와 관련된 문제이니 만큼, Java의 Queue를 활용한 방법을 구사해보고 싶었으나, Java로 문제를 풀 때 배열을 다루는 게 아직도 많이 익숙하지 않아서 방법을 도출해내지 못했다.

</br>

풀이는 다소 1차원적이다.  
이 문제를 풀면서 까다로웠던 점은, 배열의 요소들이 섞이면서 배열의 index 값도 뒤섞이게 되지만 원하는 index의 값을 기억하고 있어야 한다는 점이었다.  
이를 해결하기 위해 queue를 2차원 배열로 만들어서 queue[i][0]에는 기존 priorities의 값을, queue[i][1]에는 해당 값의 index를 넣어주었다.  
이후, queue에서 dequeue 작업을 반복 진행하면서 queue[0][1]이 내가 찾던 location이라면 반복한 횟수를 그대로 리턴하는 방식이다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(priorities, location) {
  var arr = priorities.map((priority, index) => {
    return {
      index: index,
      priority: priority,
    };
  });

  var queue = [];

  while (arr.length > 0) {
    var firstEle = arr.shift();
    var hasHighPriority = arr.some((ele) => ele.priority > firstEle.priority);
    if (hasHighPriority) {
      arr.push(firstEle);
    } else {
      queue.push(firstEle);
    }
  }

  return queue.findIndex((queueEle) => queueEle.index === location) + 1;
}
```

map 메소드를 통해 객체를 담은 배열로 변환해주었다.  
그 이후에는 나처럼 queue를 조작하면서 location을 찾아내는 것이 아니라, 비어있는 queue에 출력한 문서들을 순서대로 담아준다.  
이후에 순서대로 쌓인 queue에서 location 값을 활용해서 index를 찾아낸다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.LinkedList;

class Solution {
     public int solution(int[] priorities, int location) {
        if (priorities.length == 1) {
            return 1;
        }
        int answer = 1;
        LinkedList<Paper> papers = new LinkedList<>();
        for (int i = 0; i < priorities.length; i++) {
            papers.addLast(new Paper(i, priorities[i]));
        }

        while (true) {
            Paper paper = papers.removeFirst();
            for (Paper item : papers) {
                if (paper.priority < item.priority) {
                    papers.addLast(paper);
                    paper = null;
                    break;
                }
            }
            if (paper != null) {
                if (paper.item == location) {
                    return answer;
                } else {
                    answer++;
                }
            }
        }
    }

    class Paper {
        int item;
        int priority;

        public Paper(int item, int priority) {
            this.item = item;
            this.priority = priority;
        }
    }
}
```

Java로 이 문제를 풀려고 할 때 난감했던 부분이 `Queue<E>`를 선언할 때 Generic 타입으로 안에 뭘 넣어주어야 할지 헷갈린다는 점이었다.  
답은 간단했다.  
객체를 새로 만들어서 그것을 타입으로 활용하면 되는 것이었다! 😲  
확실히 아직도 Java 언어의 활용이 아주 많이 미숙하다는 사실을 깨닫게 되었다.  
더불어서 LinkedList의 메소드들도 낯설다.  
Queue를 선언할 때 활용하는 것이 LinkedList이기도 하고, 메소드 이름들이 딱 어떤 기능들인지 잘 유추해볼 수 있게 되어있긴 하지만, 확실하게 공부를 하고 TIL에 정리를 해야겠다.
