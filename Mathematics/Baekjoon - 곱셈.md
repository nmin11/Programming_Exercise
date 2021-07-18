## **Baekjoon > 입출력과 사칙연산 > 곱셈**

</br>

[연습 문제 링크](https://www.acmicpc.net/problem/2588)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 단계별로 풀어보기 1단계 - 입출력과 사칙연산

</br>

## 문제 요약

세 자리 수 X 세 자리 수는 다음과 같은 과정을 통해 이루어진다.

![백준 곱셈 문제](https://user-images.githubusercontent.com/75058239/126054185-e4fa21ea-01bf-4194-834b-7f79cfd81703.png)

(1)과 (2) 위치에 들어갈 세 자리 자연수가 주어질 때, (3), (4), (5), (6) 위치에 들어갈 값을 구해서 각각 출력하시오.

</br>

## 나의 풀이

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        sc.close();

        int b1 = Math.floorDiv(b, 100);
        int b2 = b - (b1 * 100);
        b2 = Math.floorDiv(b2, 10);
        int b3 = b - (b1 * 100) - (b2 * 10);

        System.out.println(b3 * a);
        System.out.println(b2 * a);
        System.out.println(b1 * a);
        System.out.println(a * b);
    }
}
```

사실, 100의 자리를 구할 때 몫은 그냥 b / 100 이런 식으로 작성해도 괜찮았지만 구글링을 해보니 floorDiv를 활용해서 몫을 구하고, floorMod를 활용해서 나머지를 구하는 것이 올바르다는 글이 있어서 이렇게 활용해보았다.  
특히 floorMod는 음수의 나머지를 구할 때 효과적이라고 한다.

</br>

이렇게 간단한 문제를 왜 올렸을까, 하는 생각이 들지도 모르겠다.  
하지만 인터넷에서 찾아 본 다른 사람의 풀이들 중에서 내가 잘 활용하지 않던 메소드를 활용해서 풀어낸 풀이가 있었다.  
그래서 나도 추후에 더 많은 메소드를 활용해보기 위해서 이렇게 정리하게 되었다.

</br>

## 다른 사람의 풀이 1

```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);

		int A = in.nextInt();
		String B = in.next();

		in.close();

		System.out.println(A * (B.charAt(2) - '0'));
		System.out.println(A * (B.charAt(1) - '0'));
		System.out.println(A * (B.charAt(0) - '0'));
		System.out.println(A * Integer.parseInt(B));

	}
}
```

Scanner를 이용해서 A는 int로, B는 String으로 입력받았다.  
그리고 B에 charAt() 메소드를 사용해서 각 자릿수를 참조했다.  
'0'이라는 문자열을 빼주는 부분은 해당 자릿수의 문자열로 들어온 숫자를 숫자로서 활용할 수 있게 해준다.

</br>

[내가 참고한 블로그](https://st-lab.tistory.com/20)에서 이 방법이 가장 대중적이라기에 놀랐다. :open_mouth:  
특히 charAt()이라는 메소드가 기능은 간단하지만 아직도 낯설다.  
Java 문제 풀이에서 더욱 많이 활용해보고 연습해보자.

</br>

## 다른 사람의 풀이 2

```java
import java.util.Scanner;

public class Main{

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);

		int A = in.nextInt();
		int B = in.nextInt();

		in.close();

		System.out.println(A*(B%10));
		System.out.println(A*(B%100/10));
		System.out.println(A*(B/100));
		System.out.println(A*B);
	}

}
```

B가 385라고 가정했을 때, 385를 10으로 나누고 나머지를 구하면 5이 된다.  
마찬가지로 385를 100으로 나누고 나머지를 구하면 85가 나오는데, 이를 다시 10으로 나누면 8이 된다.  
100의 자리는 385 / 100 을 해주면 간단하게 구할 수 있다.

</br>

내가 접근한 방식과 가장 흡사하지만 나와 같이 변수를 여러 개 더 지정하지 않고 깔끔하게 풀었다.  
나도 이제는 슬슬 효율적인 Algorithm 풀이 방법에 대해서 더 고민해볼 시간이 되었다.
