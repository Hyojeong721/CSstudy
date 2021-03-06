# Graph

### Graph?

<img src="image\그래프_그래프.png" style="zoom: 33%;" />

`비선형 자료 구조` 중 하나로 `정점`과 `간선`으로 이루어진 자료구조를 말한다.

- `비선형 자료구조`란?

  일렬로 나열하지 않고 자료 순서나 관계가 복잡한 구조를 말한다. 일반적으로 트리나 그래프를 말함.

#### Graph 특징

- 그래프는 **네트워크 모델**이다.

- 그래프는 순환(Cyclic) 혹은 비순환(Acyclic)이다.
- 그래프는 크게 방향 그래프와 무방향 그래프가 있다.

<br>

### 그래프 관련 용어

- `정점`(vertex): 위치라는 개념. (node 라고도 부름)

- `간선`(edge): 위치 간의 관계. 즉, 노드를 연결하는 선 (link, branch 라고도 부름)

- `인접 정점`(adjacent vertex): 간선에 의 해 직접 연결된 정점

- `정점의 차수`(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수

  - 무방향 그래프에 존재하는 정점의 모든 차수의 합 = 그래프의 간선 수의 2배

- 방향 그래프에서

  - 진입 차수(in-degree): 외부에서 오는 간선의 수 (내차수 라고도 부름)
  - 진출 차수(out-degree): 외부로 향하는 간선의 수 (외차수 라고도 부름)

  - 방향 그래프에 있는 정점의 진입 차수 또는 진출 차수의 합 
    = 방향 그래프의 간선의 수(내차수 + 외차수)

- 경로 길이(path length): 경로를 구성하는 데 사용된 간선의 수

- 단순 경로(simple path): 경로 중에서 반복되는 정점이 없는 경우

- 사이클(cycle): 단순 경로의 시작 정점과 종료 정점이 동일한 경우

<br>

### 그래프(Graph)의 구현 2가지

1. #### 인접 리스트(Adjacency List)

  ​	인접 리스트(Adjacency List)로 그래프를 표현하는 것이 가장 일반적인 방법이다.

  - 각각의 정점에 인접한 정점들을 리스트로 표시한 것이다. 정점의 번호만 알면 이 번호를 배열의 인덱스로 하여 각 정점의 리스트에 쉽게 접근할 수 있다.

    ```
    0: 1
    1: 2
    2: 0, 3
    3: 2
    4: 6
    5: 4
    6: 5
    ```

<br>

2. #### 인접 행렬(Adjacency Matrix)

   정점(노드)의 개수가 N인 그래프를 인접 행렬로 표현.
   간선의 수와 무관하게 항상 n^2개의 메모리 공간이 필요하다.

   ```python
   if(간선 (i, j)가 그래프에 존재)
     matrix[i][j] = 1;
   else
     matrix[i][j] = 0;
   ```

   인접 행렬에서는 인접한 노드를 찾기 위해서는 모든 노드를 전부 순회해야 하므로 효율성이 떨어짐

<br>

#### 인접 리스트 VS 인접 행렬 

##### 인접 리스트

그래프 내에 적은 숫자의 간선만을 가지는 희소 그래프(Sparse Graph) 의 경우

- 장점
  어떤 노드에 인접한 노드들 을 쉽게 찾을 수 있다.
  그래프에 존재하는 모든 간선의 수 는 O(N+E) 안에 알 수 있다. : 인접 리스트 전체를 조사한다.
- 단점
  간선의 존재 여부와 정점의 차수 : 정점 i의 리스트에 있는 노드의 수 즉, 정점 차수만큼의 시간이 필요

##### 인접 행렬

그래프에 간선이 많이 존재하는 밀집 그래프(Dense Graph) 의 경우

- 장점
  두 정점을 연결하는 간선의 존재 여부 (M [i] [j])를 O(1) 안에 즉시 알 수 있다.
  정점의 차수 는 O(N) 안에 알 수 있다. : 인접 배열의 i번 째 행 또는 열을 모두 더한다.
- 단점
  어떤 노드에 인접한 노드들을 찾기 위해서는 모든 노드를 전부 순회해야 한다.
  그래프에 존재하는 모든 간선의 수는 O(N^2) 안에 알 수 있다. : 인접 행렬 전체를 조사한다.
  



### 그래프(Graph)의 탐색

<img src="image\그래프_BFSDFS.png" style="zoom: 50%;" >



1. #### 깊이 우선 탐색(DFS, Depth-First Search)

  루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법

  즉, 넓게(wide) 탐색하기 전에 깊게(deep) 탐색하는 것이다.

  사용하는 경우: 모든 노드를 방문 하고자 하는 경우에 이 방법을 선택한다.

  깊이 우선 탐색이 너비 우선 탐색보다 좀 더 간단하다.
  **Time Complexity : O(V+E) … vertex 개수 + edge 개수**

<br>

2. #### 너비 우선 탐색(BFS, Breadth-First Search)

  루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법

  즉, 깊게(deep) 탐색하기 전에 넓게(wide) 탐색하는 것이다.

  사용하는 경우: 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.
   **Time Complexity : O(V+E) … vertex 개수 + edge 개수** ***! BFS 로 구한 경로는 최단 경로이다.***

<br>

Ex)

지구상에 존재하는 모든 친구 관계를 그래프로 표현한 후, Ash와 Vanessa 사이에 존재하는 경로를 찾는 경우.

깊이 우선 탐색의 경우 - 모든 친구 관계를 다 살펴봐야 할지도 모른다. 

너비 우선 탐색의 경우 - Ash와 가까운 관계부터 탐색

<hr>

### 예상질문

Q. 그래프와 트리의 차이점은 무엇인가요?

그래프는 정점과 간선으로 이루어진 자료구조로 네트워크 모델이고, 트리는 그래프 중 하나로 두 정점 사이에 반드시 한개의 간선(경로)만 존재하는 계층 모델입니다. 

<img src="image\그래프_그래프와트리차이.JPG" style="zoom: 67%;" />

<br>

Q. BFS, DFS 설명해보세요.

BFS, DFS 두가지 모두 그래프를 탐색하는 방법입니다. 그래프를 탐색한다는 것은 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것을 말합니다. DFS는 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식을 말합니다. BFS는 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법입니다.

<img src="image\그래프_BFSDFS구현.jpg" style="zoom:80%;" >




<hr>

참고자료

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hash-table

- https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html



