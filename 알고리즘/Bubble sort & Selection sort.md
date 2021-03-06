# Bubble sort & Selection sort

### Bubble sort

서로 인접한 두 원소를 검사하여 정렬하는 알고리즘

	- 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어있지 않으면 서료 교환한다.

선택 정렬과 기본 개념이 유사하다.

#### 예제

<img src="bubble&selection\bubble.PNG">

#### 버블 정렬(bubble sort) 알고리즘의 특징

- 장점
  - 구현이 매우 간단하다.
- 단점
  - 순서에 맞지 않은 요소를 인접한 요소와 교환한다.
  - 하나의 요소가 가장 왼쪽에서 가장 오른쪽으로 이동하기 위해서는 배열에서 모든 다른 요소들과 교환되어야 한다.
  - 특히 특정 요소가 최종 정렬 위치에 이미 있는 경우라도 교환되는 일이 일어난다.
- 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동 작업(MOVE)보다 더 복잡하기 때문에 버블 정렬은 단순성에도 불구하고 **거의 쓰이지 않는다.**

#### 버블 정렬(bubble sort)의 시간복잡도

- 비교 횟수
  최상, 평균, 최악 모두 일정
  n-1, n-2, … , 2, 1 번 = n(n-1)/2
- 교환 횟수
  입력 자료가 역순으로 정렬되어 있는 최악의 경우, 한 번 교환하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요하므로 (비교 횟수 * 3) 번 = 3n(n-1)/2
  입력 자료가 이미 정렬되어 있는 최상의 경우, 자료의 이동이 발생하지 않는다.
- T(n) = O(n^2)
  

<hr>

### Selection sort

제자리 정렬 알고리즘 중 하나로, 입력 배열 이외에 다른 추가 메모리를 요구하지 않는 정렬 방법이다.

해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘

#### 예제

<img src="bubble&selection\selection-sort.png" style="zoom:80%;" >

#### 선택 정렬(selection sort) 알고리즘의 특징

- 장점

  - 자료 이동 횟수가 미리 결정된다.

- 단점

  - 안정성을 만족하지 않는다.

    즉, 값이 같은 레코드가 있는 경우에 상대적인 위치가 변경될 수 있다.

#### 선택 정렬(selection sort)의 시간복잡도

- 비교 횟수
  두 개의 for 루프의 실행 횟수
  외부 루프: (n-1)번
  내부 루프(최솟값 찾기): n-1, n-2, … , 2, 1 번

- 교환 횟수
  외부 루프의 실행 횟수와 동일. 즉, 상수 시간 작업
  한 번 교환하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요하므로 3(n-1)번

- T(n) = (n-1) + (n-2) + … + 2 + 1 = n(n-1)/2 = O(n^2)

  

#### 정렬 알고리즘 시간복잡도

<img src="bubble&selection\sort-time-complexity.png">

<hr>

bubble sort 출처

https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html

selection sort 출처

https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html