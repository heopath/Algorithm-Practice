# Algorithm Practice

Java로 코딩테스트를 준비하며 푼 문제와 학습 기록을 남기는 저장소입니다.

- **시작** 2026-09-04
- **언어** Java
- **주 플랫폼** [프로그래머스](https://school.programmers.co.kr/learn/challenges)
- **목표** 프로그래머스 Lv.2 안정 통과
- **기록** [LOG.md](LOG.md)

---

## 연습 사이트

**백준(BOJ)은 2026년 4월 28일자로 채점 서비스를 중단했다.** 현재 문제 제출이 불가능하며,
공지에는 "채점 서비스와 함께 곧 다시 돌아오겠다"고 되어 있다. 재개되면 보조로 쓴다.
solved.ac는 BOJ 채점에 의존하므로 함께 사용할 수 없다.

그래서 **프로그래머스를 주 플랫폼으로 삼는다.** 국내 기업 코딩테스트가 대부분
프로그래머스 형식이라 실전 화면에 익숙해지는 이점도 있다.

| 사이트 | 용도 | 비고 |
|---|---|---|
| [프로그래머스](https://school.programmers.co.kr/learn/challenges) | 메인 | 무료. 국내 코테 표준 |
| [구름LEVEL](https://level.goorm.io) | 보충 | 무료. 국내 기업 코테 플랫폼으로도 사용됨 |
| [SW Expert Academy](https://swexpertacademy.com) | 보충 | 무료. 삼성 계열 |
| [코드트리](https://www.codetree.ai) | 선택 | 유료. 커리큘럼형이라 순서대로 따라가기 좋음 |

---

## 원칙 3가지

**1. 하루 2문제** — 새 문제 1개 + 예전에 틀린 문제 1개. 하루 2~3시간.

**2. 30분 룰** — 30분 고민해서 접근법이 안 떠오르면 바로 해설을 본다.
대신 조건이 있다. 해설을 봤으면 **그날 안에 아무것도 안 보고 처음부터 다시 구현**하고, **3일 뒤 한 번 더** 푼다.
초보 단계에서 한 문제를 3시간 붙잡는 것은 공부가 아니라 시간 낭비다.

**3. 매일 커밋** — 못 푼 날도 기록만 남긴다. 잔디는 실력이 아니라 습관의 증거다.

---

## Java 입출력 규칙 (필수)

프로그래머스는 함수 구현 방식이라 입출력을 직접 다루지 않지만,
구름LEVEL·SWEA와 기업 코테 일부는 표준 입력을 직접 받는다.

이때 `Scanner`를 쓰면 입력이 많은 문제에서 **알고리즘이 맞아도 시간 초과로 틀린다.**
출력도 반복문 안에서 `System.out.println`을 부르지 말고 `StringBuilder`에 모아 마지막에 한 번만 출력한다.

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        // ...

        System.out.print(sb);
    }
}
```

---

## 4주 커리큘럼

### 1주차 — 손 풀기
[코딩테스트 입문(Lv.0)](https://school.programmers.co.kr/learn/courses/30/parts/12198)과 Lv.1 문제들.
배열, 문자열, 반복문, 조건문 위주다.
개념보다 **Java 문법과 자료형에 손이 다시 붙는 것**이 목적이다.

- [ ] Lv.0 코딩 기초 트레이닝 진행
- [ ] Lv.1 문제 10개 이상
- [ ] `String`, `char`, `int[]`, `List`, `Map` 변환에 막히지 않기

### 2주차 — 자료구조
[고득점 Kit](https://school.programmers.co.kr/learn/challenges?tab=algorithm_practice_kit)의 해시 · 스택/큐 · 정렬.

특히 **해시(HashMap)를 확실히** 해둔다. 코테 출제 빈도가 높고,
"무엇을 키로 잡을 것인가"는 실무의 캐시 키 설계와 같은 사고방식이다.

- [ ] 해시
- [ ] 스택 / 큐
- [ ] 정렬

### 3주차 — BFS / DFS (가장 중요)
[고득점 Kit — 깊이/너비 우선 탐색](https://school.programmers.co.kr/learn/challenges?tab=algorithm_practice_kit).
**코테 출제 빈도 1위**이며 여기서 막히면 대부분 떨어진다. 한 주를 통째로 쓴다.

- **BFS** 한 칸씩 퍼져나가며 최단거리를 찾는 방식 — `Queue` 사용
- **DFS** 한 방향으로 끝까지 파고들었다가 되돌아오는 방식 — 재귀 또는 `Stack`

- [ ] 고득점 Kit 깊이/너비 우선 탐색 전 문제
- [ ] 2차원 격자 탐색(상하좌우 이동) 패턴 손에 익히기
- [ ] 고득점 Kit 완전탐색

### 4주차 — 그리디 + DP 기초
**그리디**는 매 순간 제일 좋아 보이는 것을 고르는 방식. 쉽고 자주 나온다.
**DP**는 어렵다. 여기서 욕심내지 않는다. 기본 패턴만 익히고 넘어간다.

- [ ] 고득점 Kit 탐욕법(Greedy)
- [ ] 고득점 Kit 동적계획법(DP) — 기본형 위주
- [ ] 고득점 Kit 이분탐색

---

## 유형 우선순위

| 우선순위 | 유형 |
|---|---|
| **필수** | 구현·시뮬레이션, 문자열, 정렬, 해시, 스택/큐, 완전탐색, **BFS/DFS**, 그리디 |
| **여유되면** | 이분탐색, 투포인터, DP 기초 |
| **후순위** | 다익스트라(최단경로), 유니온파인드 |

### 하지 않는 것

시간을 아끼기 위해 명확히 제외한다. 일반적인 코테 범위를 벗어난다.

- 세그먼트 트리 / 펜윅 트리
- 네트워크 플로우
- 최소 스패닝 트리(MST)
- 위상 정렬

"코테 필수 알고리즘 30선" 같은 목록에는 이런 것이 다 들어 있지만,
그것은 상위권 공채나 경력직 기준이다.

---

## 디렉터리

```
solutions/
├── week1-basic/            Lv.0 · Lv.1 기초
├── week2-datastructure/    해시·스택/큐·정렬
├── week3-bfs-dfs/          그래프 탐색·완전탐색
└── week4-greedy-dp/        그리디·DP·이분탐색
```

파일명은 `PGS_해시_완주하지못한선수.java` 형식으로 통일한다.
백준 재개 시에는 `BOJ_1260_DFS와BFS.java` 형식을 함께 사용한다.
