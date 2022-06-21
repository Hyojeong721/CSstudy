# **Array vs. Linked List**

## **Array (배열)**

<인덱스, 요소> 쌍의 집합

### **특징**

- 정의와 동시에 길이를 지정하며 길이를 바꿀 수 없다.
- 인덱스를 가진다.
- 인덱스를 활용하여 빠르게 조회가 가능하다. -> **시간복잡도 O(1)**
- `cache hit`의 가능성이 커져서 성능에 큰 도움이 된다.
- 삭제된 element이 공간이 그대로 남는다 -> 메모리의 낭비

### **한계**

- 길이를 바꿀 수 없다

  - 가변 배열(원소의 삽입, 삭제)의 경우 리소스 낭비가 크다. **시간복잡도 O(n)**

  -> 이런 한계를 해결하기 위해 `linked list`를 사용한다.

## **Linked List**

![image](https://user-images.githubusercontent.com/97162920/174086862-6150c3a1-b694-47fc-a22d-5bcb950151d1.png)

- 배열이 가진 인덱스라는 장점을 버림
- 빈틈없는 데이터의 적재
- 순서가 있는 데이터의 모임
- 순차성을 보장하지 않는다 -> cache hit가 어렵다.
- 데이터 개수가 정해져있고 자주 사용된다면 array가 더 효율적이다.
- **시간복잡도 O(n)**
  - 시간복잡도 측면에서는 이득이 없지만 메모리를 낭비하지 않고 삽입, 삭제의 구현이 쉽다.

---

> 배열에서 인덱스 - 유일무이한 식별자
>
>
> 리스트에서 인덱스 - 몇번째 데이터인가

> 인덱스가 중요한 경우는 배열을, 인덱스가 중요하지 않은 경우는 리스트를 사용한다

> cache hit란?
>
>
> CPU가 참조하고자 하는 메모리가 캐시에 존재하는 경우



<br>

<br>

# **Stack and Queue**

## **Stack**

![https://images.velog.io/images/tiiranocode/post/0c3b8a68-f29c-4836-91ff-2f0ef25dc704/stack.png](https://images.velog.io/images/tiiranocode/post/0c3b8a68-f29c-4836-91ff-2f0ef25dc704/stack.png)

**후입선출(LIFO: Last-In First-Out)** 의 형식으로 입출력이 일어나는 자료 구조.

## **Queue**

![https://velog.velcdn.com/images%2Ftiiranocode%2Fpost%2F93d6b6c5-5861-4077-a7df-12a9fae18fb7%2Fqueue.png](https://velog.velcdn.com/images%2Ftiiranocode%2Fpost%2F93d6b6c5-5861-4077-a7df-12a9fae18fb7%2Fqueue.png)

**선입선출(FIFO: First-In First-Out)** 의 형식으로 입출력이 일어나는 자료구조

<br>

<br>

# **Tree**

## **Tree**

비선형 구조. 계층적 관계를 표현하는 자료구조.

![https://velog.velcdn.com/images%2Fdeannn%2Fpost%2F3e04f457-74c1-4139-b748-af3858ce1fb6%2F9975E4375BDD3BFF3A.png](https://velog.velcdn.com/images%2Fdeannn%2Fpost%2F3e04f457-74c1-4139-b748-af3858ce1fb6%2F9975E4375BDD3BFF3A.png)

### **관련 용어**

노드, 간선(edge), 루트노드, 단말노드, 레벨(깊이), 높이, 부모노드, 자식노드, 형제노드, 노드의 크기, 노드의 차수, 트리의 차수.

### **특징**

- 사이클이 존재하지 않는다.
  - 사이클 존재 -> 그래프
- 루트에서 어떤 한 노드로 가는 경로는 유일하다.
- 노드의 개수가 N개이면 간선의 개수는 N-1개 이다.

## **순회 방식**

![https://velog.velcdn.com/images%2Fdeannn%2Fpost%2F7456c0ce-0aef-4bae-bcb0-1e6bf5759291%2Fimage.png](https://velog.velcdn.com/images%2Fdeannn%2Fpost%2F7456c0ce-0aef-4bae-bcb0-1e6bf5759291%2Fimage.png)

- 전위 순회(pre-order)
  - 루트 노드 -> 왼쪽 하위 트리 -> 오른쪽 하위 트리
  - `1 -> 2 -> 4 -> 8 -> 9 -> 5 -> 10 -> 11 -> 3 -> 6 -> 13 -> 7 -> 14`
- 중위 순회(in-order)
  - 왼쪽 하위 트리 -> 루트노드 -> 오른쪽 하위 트리
  - `8 -> 4 -> 9 -> 2 -> 10 -> 5 -> 11 -> 1 -> 6 -> 13 -> 3 -> 14 -> 7`
- 후위 순회(post-order)
  - 왼쪽 하위 트리 -> 오른쪽 하위 트리 -> 루트 노드
  - `8 -> 9 -> 4 -> 10 -> 11 -> 5 -> 2 -> 13 -> 6 -> 14 -> 7 -> 3 -> 1`
- 레벨 순위
  - 루트노드부터 계층별로 방문
  - `1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11 -> 13 -> 14`

## **Binary Tree 이진트리**

![image](https://user-images.githubusercontent.com/97162920/174087827-1e42380f-0c3b-44ce-9211-bfd610de4656.png)


- 각 노드가 최대 두개의 자식 노드를 가지는 트리.
- 이진트리에는 서브트리간의 순서가 존재한다.
  - 왼쪽 서브트리와 오른쪽 서브트리는 서로 구별된다.
- 일반 트리와 달리 이진트리는 노드를 하나도 갖지 않을 수 있다.
- 포화 이진 트리, 완전 이진 트리, 기타 이진 트리, 경사 이진 트리

## **BST (Binary Search Tree) 이진 탐색 트리**

![image](https://user-images.githubusercontent.com/97162920/174088358-39dce9ca-cd20-4fca-8ff6-63b5a9cafc98.png)

이진 트리 기반의 탐색을 위한 자료구조.

- 모든 노드의 키는 유일하다.

- **왼쪽 서브 트리의 키값들은 루트의 키값보다 작다.**

- **오른쪽 서브 트리의 키값들은 루트의 키값보다 크다.**

- 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.

- 포화 이진 탐색 트리일 때 최선의 탐색 성능을 낸다.

- **시간복잡도: O(log n)**

  *편향트리의 경우 O(n)*

<br>

<br>

CS study : Binary Heap

>[Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner)/**DataStructure**/

- 위 repository 를 읽고 정리한 글입니다. 



## ADT Priority Queue

- 3가지 동작이 가능한 Queue

1. `insertion`

2. `deletion`, `retrieval` of max element

- `array`, `linked list`, `search tree`, `heap` 을 통해 구현 가능하다. 



## Binary Heap

### 정의

트리 구조

- 그 중에서도 배열로 표현가능한 `완전 이진 트리(Complete Binary Tree)` 이며, 
  - 완전 이진 트리는, 루트로부터 시작해서 가능한 지점까지 모든 노드가 정확히 두 개씩의 자식 노드를 가지며, 노드의 수가 부족해 `포화 이진 트리(Full Binary Tree)`가 안되는 경우엔, 맨 마지막 레벨은 왼쪽부터 채워나간다.  



`힙(Heap)` 에는 `최대힙 (Max Heap)` 과 `최소힙(Min Heap)` 두 종류가 있다. 

- 최대힙은, 각 노드의 값이 해당 노드의 자식 노드의 값보다 크거나 같다. 
  - 최대힙에선, 루트 노드에 있는 값이 가장 크므로, 최댓값을 찾는데 소요되는 연산의 시간 복잡도가 `O(1)` 이다.
- 최소힙은, 각 노드의 값이 해당 노드의 자식 노드의 값보다 작거나 같다. 



<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/1707px-Max-Heap.svg.png" alt="max-heap" style="zoom: 25%;"/>

완전 이진 트리는 배열로 표현 가능하므로 인덱스가 `i` 인 노드의 

- 자식은 `2i + 1`, `2i + 2` 에 존재하고, 
- 부모는 `(i - 1) // 2` 에 존재한다. 

만약 배열의 0번 인덱스를 건너뛰고, 1번 자리부터 사용하면, 자식은 `2i`, `2i + 1` 부모는 `i//2` 번째에 존재한다. 



>정리하면.. 
>
>1. 완전 이진 트리 구조를 가지며, 최대힙과 최소힙으로 나눌 수 있다. 
>2. 최대힙은 각 노드의 값이 해당 노드의 자식 노드 값보다 크거나 같고, 따라서 루트 노드의 값이 가장 크다. 
>3. 따라서 최댓값 혹은 최솟값을 찾는 연산의 시간 복잡도가 `O(1)` 이므로, 우선 순위 큐 구현에 사용하면 효율적이다. 



### Heap 객체 구현

- 필드 

  - `A[]` : heap 원소들이 저장되는 배열 
  - `numItems` : heap 에 있는 원소의 총 수 

- 작업

  - `insert(x)` : heap 에 원소 x 를 삽입한다. 
  - `deleteMax()` : heap 의 최대 원소를 알려주면서 삭제한다. 
  - `max()` heap 의 최대 원소를 알려준다. 
  - `buildHeap()` : 배열 A[] 를 heap 으로 만든다. 
  - `isEmpty()` : heap 이 빈 heap 인지 알려준다. 
  - `clear()` : heap 을 깨끗이 청소한다. (비운다)

  

#### Deletion

1. Return the root item 
2. Remove the last node and move it to the root 
3. Percolate down until the heap is valid 

수행 시간은 최악의 경우 `θ(logn)` , 최선의 경우 `θ(1)` 

#### Insertion 

1. Insert an item into the bottom of the complete tree
2. Percolate up until the heap is valid 

수행 시간은 최악의 경우 `θ(logn)` , 최선의 경우 `θ(1)` 

#### buildHeap 

임의의 배열이 주어진 상황에서, 맨 마지막 노드의 parent 부터 시작하여, 그 앞의 약 `n/2` 개의 노드에 대해 교환을 시도한다. 

수행시간 `θ(n)` 



### Heap sort

임의의 배열을 `buildHeap` 을 통해 힙 자료구조로 만든 뒤, `deletion` 작업을 수행하며 얻은 최댓값을 다시 배열에 차례대로 집어 넣는다. 

수행시간은 `O(nlogn)`, 최악의 경우 `θ(nlogn)`





## Red Black Tree 

### 정의

Balanced Binary Search Tree 로, AVL Tree 와 함께, `search`, `insertion`, `deletion` 에 `O(nlogn)` 의 시간복잡도를 보장한다. 

Binary Search Tree 는 같은 데이터를 가지고도, 다른 형태의 트리 모양을 가질 수 있는데, 한 쪽으로 치우친 편향 트리의 경우엔 성능이 좋지 않다. 

따라서 모양을 compact 하게 구성하여 효율적인 트리를 구성해야 하는데, 이를 적용한 것이 Balanced Binary Search Tree 이다.  

아래의 성질을 만족한다. 

![레드-블랙 트리 - 위키백과, 우리 모두의 백과사전](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/500px-Red-black_tree_example.svg.png)

1. 모든 null 자리에 리프 노드를 두며, RB-Tree에서 리프 노드는 이 null 리프 를 말한다
2. 모든 노드는 `red` 또는 `black`이라는 색깔을 갖는다.
3. Root node 의 색깔은 `black`이다.
4. 각 leaf node 는 `black`이다.
5. 어떤 노드의 색깔이 `red`라면 두 개의 children 의 색깔은 모두 black 이다.
   - 즉, 루트로부터 임의의 리프 노드에 이르는 경로 상에 `red` 노드 두 개가 연속해서 출현하지 못한다. 
6. 루트 노드에서 임의의 리프 노드에 이르는 경로에서 만나는 `black` 노드의 수는 모두 같다. 이를 해당 노드의 `Black-Height`라고 한다.

Java Collection 에서 TreeMap 도 내부적으로 RBT 로 이루어져 있고, HashMap 에서의 `Separate Chaining`에서도 사용된다. 그만큼 효율이 좋고 중요한 자료구조이다.

### 구현

#### Insertion 

일반적인 BST 의 삽입 작업을 수행하고, 삽입한 노드에 `red` 를 칠하고, 삽입한 노드의 좌우에 null 리프를 달아준다. 

1. 삽입한 노드의 부모 노드가 `black` 인 경우 

   - 수선이 필요하지 않다. 

2. 삽입한 노드의 부모 노드가 `red` 인 경우

   - 수선이 필요 

    ![image-20220616204611399](C:\Users\USER\Desktop\CSstudy\자료구조\Binary_Heap.assets\image-20220616204611399.png)



#### Rebalancing

정의에서 살펴본 5, 6번 성질을 만족하도록 수선 필요. 

<br>

<br>

# Hash Table

### 정의

해시 테이블은 (key, value)로 데이터를 저장하는 자료구조 중 하나.

<br>

#### 특징

`Hash`는 내부적으로 `배열(버킷)`을 사용하여 데이터를 저장하기 때문에 **빠른 검색 속도**를 갖는다.

- 각 Key 값에 `해시함수`를 적용해 데이터 고유의 `인덱스`로 접근하기 때문에 평균 시간 복잡도가 O(1)이 되는 것이다. (항상 O(1)은 아님.)

- `배열(버킷)` = 실제 값이 저장되는 장소


<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\image-20220616135542550.png" />



​	Ex) 

```
예를 들어 우리가 (Key, Value)가 ("John Smith", "521-1234")인 데이터를 크기가 16인 해시 테이블에 저장한다고 하자. 
그러면 먼저 index = hash_function("John Smith") % 16 연산을 통해 index 값을 계산한다. 
그리고 array[index] = "521-1234" 로 전화번호를 저장하게 된다.
```

<br>

### Hash 함수(해시함수)

```
'특별한 알고리즘'이란 것을 통해 고유한 인덱스 값을 설정하는 것 
=> '특별한 알고리즘' = `해시함수`, hash method
```

저장되는 값들의 key 값을 `해시함수`를 통해서 **작은 범위의 값들**로 바꿔준다.

`hashcode` : 해시 함수에 의해 반환된 데이터의 고유 숫자 값

`hashing` : 해시 함수를 통해 계산됨을 의미

<br>

#### 좋은 해시함수는?

- key의 전체를 참조하여 해쉬 값을 만들어 낸다. (key의 일부분을 참조하여 해쉬 값을 만들지 않음)

- 무조건 1:1로 만드는 것은 거의 불가능이므로 Collision을 최소화하는 방향으로 설계 + 발생하는 Collision에 적절한 대응
  - Collision이 많아질수록  Time Complexity 가 O(1)에서 O(n)에 가까워지므로 좋은 해시함수를 선택해야 함
- hash table의 성능 향상에 필수적

<br>

#### Conflict 해결법

##### 1. 분리 연결법(Separate Chaining)

```
Separate Chaining이란 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장하는 것이다.
```

<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\해쉬_분리연결법.JPG" style="zoom: 67%;" />

동일한 버킷으로 접근하면 데이터들을 연결해서 관리해주는 것.

<br>

- **연결 구현 방식** 
  => 하나의 해시 버킷에 할당된 key-value 쌍의 개수를 기준으로 
  	적다면 linked list, 많다면 Tree

  =>  key-value 쌍의 기준 개수 = 6개, 8개 (자료구조 변경기준이1이면 Switching 비용 큼)

  - `Linked List`(연결 리스트를 사용하는 방식)
    - 각각의 버킷(bucket)들을 연결리스트(Linked List)로 만들어 Collision 이 발생하면 해당 bucket 의 list 에 추가하는 방식
  - `Red-Black Tree`(Tree를 사용하는 방식)
    - 기본적인 알고리즘은 Separate Chaining 방식과 동일하며 연결 리스트 대신 트리를 사용하는 방식
    - 트리는 기본적으로 메모리 사용량이 많기 때문에 데이터 개수가 적을 때 Worst Case 를 살펴보면 트리와 링크드 리스트의 성능 상 차이가 거의 없다. 따라서 메모리 측면을 봤을 때 데이터 개수가 적을 때는 링크드 리스트를 사용한다.

<br>

- **보조 해시 함수**

  보조 해시 함수(supplement hash function)의 목적은 key의 해시 값을 변형하여 **해시 충돌 가능성을 줄이는 것**이다. `Separate Chaining` 방식을 사용할 때 함께 사용되며 보조 해시 함수로 Worst Case 에 가까워지는 경우를 줄일 수 있다.

<br>

하지만 데이터의 수가 많아지면 동일한 버킷에 chaining되는 데이터가 많아지며 그에 따라 캐시의 효율성이 감소한다는 단점이 있다.

<br>

##### 2. 개방 주소법(Open Addressing)

```
Open Addressing이란 추가적인 메모리를 사용하는 Chaining 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법이다.
```

- **Open Addressing 구현 방식**
  - Linear Probing: 순차적으로 탐색하며 비어있는 버킷을 찾을 때까지 계속 진행된다.
  - Quadratic Probing: 2 차 함수를 이용해 탐색할 위치를 찾는다.
  - Double Hashing Probing: 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식이다. 해시된 값을 한번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산을 하게 된다.

Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에 Hash Table을 재정리 해주는 작업이 필요하다고 한다.

<br>

##### Separate Chaining  VS  Open Address

일단 두 방식 모두 Worst Case 에서 O(M)이다. 

- 데이터의 개수가 충분히 적다면?
  - open Address가 성능이 좋다. 연속된 공간에 데이터를 저장하기 때문에 캐시 효율이 높다.

<br>

#### 해시 버킷 동적 확장(Resize)

해시 버킷의 개수가 적다면 메모리 사용을 아낄 수 있지만 해시 충돌로 인해 성능 상 손실이 발생한다.

- HashMap

  key-value 쌍 데이터 개수가 `일정 개수 이상`이 되면 해시 버킷의 개수를 두 배로 늘린다.

  충돌로 인한 성능 손실 문제를 어느 정도 해결 가능.

  - `일정 개수 이상` 
    : 현재 데이터 개수가 해시 버킷의 개수의 75%가 될 때. ( load factor = `0.75`)



<hr>


### 예상질문

Q. 해시테이블을 설명하세요.

해시 테이블은 무한에 가까운 데이터(키)들을 유한한 개수와 해시 값으로 매핑한 테이블입니다.

이를 통해 작은 크기의 캐시 메모리로도 프로세스를 관리할도록 할 수 있습니다.



<hr>


참고자료

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hash-table

- https://mangkyu.tistory.com/102 [MangKyu's Diary:티스토리]

<br>

<br>

# Graph

### Graph?

<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\그래프_그래프.png" style="zoom: 33%;" />

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

<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\그래프_BFSDFS.png" style="zoom: 50%;" >



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

<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\그래프_그래프와트리차이.JPG" style="zoom: 67%;" />

<br>

Q. BFS, DFS 설명해보세요.

BFS, DFS 두가지 모두 그래프를 탐색하는 방법입니다. 그래프를 탐색한다는 것은 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것을 말합니다. BFS는 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식을 말합니다. BFS는 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법입니다.

<img src="C:\Users\USER\Desktop\CSstudy\자료구조\image\그래프_BFSDFS구현.jpg" style="zoom:80%;" >




<hr>


참고자료

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hash-table

- https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html



