## **Programmers > 해시 > 베스트앨범**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42579)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 3

</br>

## 문제 요약

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 **두 개씩 모아** 베스트 앨범을 출시하려 한다.  
노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같다.

1. Genre 내 곡들의 전체 재생 횟수에 따라 Genre들을 내림차순으로 정렬해서 수록
2. Genre 내에서도 가장 많이 재생된 노래를 먼저 수록
3. Genre 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록

노래의 Genre를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 리턴하라.

</br>

## 추가 사항

- genres[i]는 고유 번호가 i인 노래의 장르
- plays[i]는 고유 번호가 i인 노래가 재생된 횟수
- 1 <= genres.length = plays.length <= 10,000
- Genre의 종류는 100개 미만
- **Genre에 속한 곡이 하나라면, 하나의 곡만 선택**
- **모든 장르는 재생된 횟수가 다름**

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.*;

class Solution {

    static class Music {
        String genre;
        int play;
        int index;

        public Music(String genre, int play, int index) {
            this.genre = genre;
            this.play = play;
            this.index = index;
        }
    }

    public int[] solution(String[] genres, int[] plays) {
        HashMap<String, Integer> map = new HashMap<>();
        for (int i = 0; i < genres.length; i++) {
            map.put(genres[i], map.getOrDefault(genres[i], 0) + plays[i]);
        }

        ArrayList<String> sortedGenres = new ArrayList<>();
        while (map.size() != 0) {
            int max = -1;
            String maxKey = "";
            for (String key : map.keySet()) {
                int tmp = map.get(key);
                if (tmp > max) {
                    max = tmp;
                    maxKey = key;
                }
            }
            sortedGenres.add(maxKey);
            map.remove(maxKey);
        }

        ArrayList<Music> result = new ArrayList<>();
        for (String genre : sortedGenres) {
            ArrayList<Music> list = new ArrayList<>();
            for (int i = 0; i < genres.length; i++) {
                if (genres[i].equals(genre)) {
                    list.add(new Music(genre, plays[i], i));
                }
            }
            Collections.sort(list, (el1, el2) -> el2.play - el1.play);
            result.add(list.get(0));
            if (list.size() != 1) {
                result.add(list.get(1));
            }
        }

        int[] answer = new int[result.size()];
        for (int i = 0; i < result.size(); i++) {
            answer[i] = result.get(i).index;
        }
        return answer;
    }

}
```

풀이 방식은 이렇다.  
우선 HashMap에 Genre와, 해당 Genre에 속한 모든 곡들의 재생 횟수를 더한 값을 넣어준다.  
이후 ArrayList를 통해서 Genre들을 전체 재생 횟수를 내림차순하여 정렬해 놓는다.  
그 다음, Music 클래스를 타입으로 가지는 ArrayList를 만들어서 Music 타입 요소들을 역시 재생 횟수에 따라 내림차순 정렬하면서 넣어준다.  
이 때, 해당 Genre에 속한 곡이 1곡만 있으면 1곡만 집어넣고, 2곡 이상이라면 2곡을 넣어준다.  
마지막으로, ArrayList에서 index값만 다시 배열 타입으로 변형해서 넣어주고 리턴해준다.

</br>

이 문제와 같이 프로그래머스의 해시 관련 문제였던 [위장](https://github.com/nmin11/Programming_Exercise/blob/main/Hash%20Table/Programmers%20-%20%EC%9C%84%EC%9E%A5.md) 문제를 풀지 못했어서 이 문제는 꼭 풀어보고 싶은 마음이 동했지만, 아쉽게도 풀어내지 못했다.  
상당히 오랜 시간을 들여서 문제를 풀어보았지만, 내 능력 밖의 문제라고 생각했고, 검색을 통해서 풀이를 확인했다. [(참고한 블로그)](https://velog.io/@yanghl98/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%B2%A0%EC%8A%A4%ED%8A%B8%EC%95%A8%EB%B2%94-JAVA%EC%9E%90%EB%B0%94)  
전체적인 풀이의 접근 방식은 내가 생각했던 방식과도 유사했다.  
그래서 아쉬움이 많이 남는다.  
하지만 내가 계속 풀었어도 Music 클래스를 따로 생성해서 ArrayList의 타입으로 활용한다는 생각을 끝내 하지 못했을 것이다.  
Music 클래스를 통해서 필요한 자료들을 간단하게 기억해주는 방식이 인상깊었다.  
예전에 Stack과 Queue 문제를 풀 때도 이렇게 자료형을 직접 만들어주는 방식을 분명히 한 번 봤음에도 이러한 방법을 연상해내지 못했다.  
사실 문제 자체가 꽤나 난이도가 있는 문제였지만, 그래도 부끄러움과 속상함이 남는다.  
이미 짚어보고 넘어간 문제라 하여도, 다시 들여다보고, 필요하면 다시 풀어보고 하면서 확실히 공부를 해놔야겠다는 생각이 든다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(genres, plays) {
  var songs = genres.map((genre, index) => {
    return {
      no: index,
      genre: genre,
      playCount: plays[index],
    };
  });

  var genrePlayCount = [];
  songs.forEach((song) => {
    var thisGenre = genrePlayCount.find(
      (genrePlay) => genrePlay.genre === song.genre
    );
    if (!thisGenre) {
      genrePlayCount.push({
        genre: song.genre,
        totalPlayCount: song.playCount,
      });
    } else {
      thisGenre.totalPlayCount += song.playCount;
    }
  });

  genrePlayCount.sort((a, b) => b.totalPlayCount - a.totalPlayCount);

  var answer = [];
  genrePlayCount.forEach((genrePlay) => {
    var thisGenreSongs = songs.filter((song) => genrePlay.genre === song.genre);
    thisGenreSongs.sort((a, b) => b.playCount - a.playCount);
    answer.push(thisGenreSongs[0].no);
    if (thisGenreSongs.length > 1) {
      answer.push(thisGenreSongs[1].no);
    }
  });

  return answer;
}
```

Java의 코드와 모양새는 꽤 다르지만 유심히 들여다보면 똑같이 접근했음을 확인할 수 있었다.  
객체 타입을 요소로 갖는 배열을 활용하여, Java에서 했던 `ArrayList<Music>` 과 같은 역할을 하게 해준 것이다.  
같은 로직이라고 대충 보고 넘어갈 것이 아니라, 몇 번 더 살펴보면서 객체의 활용 방식에 대해 충분히 학습해두자.
