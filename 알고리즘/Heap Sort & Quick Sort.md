## Heap Sort

`binary heap` 자료구조를 활용할 Sorting 방법에는 두 가지 방법이 존재한다. 하나는 정렬의 대상인 데이터들을 힙에 넣었다가 꺼내는 원리로 Sorting 을 하게 되는 방법이고, 나머지 하나는 기존의 배열을 `heapify`(heap 으로 만들어주는 과정)을 거쳐 꺼내는 원리로 정렬하는 방법이다. `heap`에 데이터를 저장하는 시간 복잡도는 `O(log n)`이고, 삭제 시간 복잡도 또한 `O(log n)`이 된다. 때문에 힙 자료구조를 사용하여 Sorting 을 하는데 time complexity 는 `O(log n)`이 된다. 이 정렬을 하려는 대상이 n 개라면 time complexity 는 `O(nlogn)`이 된다.



#### heapify

주어진 자료구조에서 힙 성질을 만족하도록 하는 연산을`heapify`라고 한다. `heapify`의 계산복잡성은 O(logn)이다.



| Space Complexity | Time Complexity |
| ---------------- | --------------- |
| O(1)             | O(nlogn)        |

즉, heap Sort는 heap 자료구조를 활용한 Sorting 방법으로 완전이진트리를 자료구조를 기본으로 한다.



heap : https://github.com/Hyojeong721/CSstudy/blob/main/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/Binary_Heap_and_RB_Tree.md



## Quick Sort

**분할 정복** 알고리즘의 하나로, 평균적으로 매우 빠른 수행속도를 자랑하는 정렬 방법이다.

퀵 정렬은 불안정 정렬에 속하며 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다.





##### 분할 정복(divide and conquer) 방법

문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다. 

분할 정복 방법은 대개 순환 호출(재귀) 을 이용하여 구현한다.



#### 과정 설명

1. 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 피벗(pivot) 이라고 한다.

   ​

2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다. (피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)

   ​

3. 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.

- 분할된 부분 리스트에 대하여 순환 호출 을 이용하여 정렬을 반복한다.


- 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.

  ​

4. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.

- 리스트의 크기가 0이나 1이 될 때까지 반복한다.

![quick-sort-concepts](C:\cs-study\퀵 정렬\image\quick-sort-concepts.png)





#### 퀵 정렬(quick sort)의 시간복잡도



#### 최선의 경우

##### 비교 횟수

![최선](C:\cs-study\퀵 정렬\image\최선.png)

- 순환 호출의 깊이

  - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, n=2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 n=2^k의 경우, k(k=log₂n)임을 알 수 있다.
  - k=log₂n

  ​

- 각 순환 호출 단계의 비교 연산

  - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
  - 평균 n번

- 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = nlog₂n

##### 이동 횟수

- 비교 횟수보다 적으므로 무시할 수 있다.

  ​

**최선의 경우 T(n) = O(nlog₂n)**



#### 최악의 경우

리스트가 계속 불균형하게 나누어지는 경우 (특히, 이미 정렬된 리스트에 대하여 퀵 정렬을 실행하는 경우)

##### 비교 횟수

![최악](C:\cs-study\퀵 정렬\image\최악.png)

- 순환 호출의 깊이
  - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, 순환 호출의 깊이는 n임을 알 수 있다.
  - n
- 각 순환 호출 단계의 비교 연산
  - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
  - 평균 n번
- 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = n^2

##### 이동 횟수

- 비교 횟수보다 적으므로 무시할 수 있다.

**최악의 경우 T(n) = O(n^2)**



#### 평균

**평균 T(n) = O(nlog₂n)**

시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
퀵 정렬이 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문이다.



| Space Complexity | Time Complexity |
| ---------------- | --------------- |
| O(log(n))        | O(nlogn)        |