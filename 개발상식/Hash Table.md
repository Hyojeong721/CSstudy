# Hash Table

### 정의

해시 테이블은 (key, value)로 데이터를 저장하는 자료구조 중 하나.

<br>

#### 특징

`Hash`는 내부적으로 `배열(버킷)`을 사용하여 데이터를 저장하기 때문에 **빠른 검색 속도**를 갖는다.

- 각 Key 값에 `해시함수`를 적용해 데이터 고유의 `인덱스`로 접근하기 때문에 평균 시간 복잡도가 O(1)이 되는 것이다. (항상 O(1)은 아님.)

- `배열(버킷)` = 실제 값이 저장되는 장소

![](C:\Users\USER\Desktop\CSstudy\개발상식\image\image-20220616135542550.png)

​	Ex) 

```
예를 들어 우리가 (Key, Value)가 ("John Smith", "521-1234")인 데이터를 크기가 16인 해시 테이블에 저장한다고 하자. 그러면 먼저 index = hash_function("John Smith") % 16 연산을 통해 index 값을 계산한다. 그리고 array[index] = "521-1234" 로 전화번호를 저장하게 된다.
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



#### 좋은 해시함수는?

- key의 전체를 참조하여 해쉬 값을 만들어 낸다. (key의 일부분을 참조하여 해쉬 값을 만들지 않음)

- 무조건 1:1로 만드는 것은 거의 불가능이므로 Collision을 최소화하는 방향으로 설계 + 발생하는 Collision에 적절한 대응
  - Collision이 많아질수록  Time Complexity 가 O(1)에서 O(n)에 가까워지므로 좋은 해시함수를 선택해야 함
- hash table의 성능 향상에 필수적



#### Conflict 해결법

##### 1. 분리 연결법(Separate Chaining)

```
Separate Chaining이란 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장하는 것이다.
```



<img src="C:\Users\USER\Desktop\CSstudy\개발상식\image\해쉬_분리연결법.JPG" style="zoom: 67%;" />

동일한 버킷으로 접근하면 데이터들을 연결해서 관리해주는 것.

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

<br>

Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에 Hash Table을 재정리 해주는 작업이 필요하다고 한다.

<br>

##### `Separate Chaining` vs`Open Address` 

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

참고자료

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hash-table

- https://mangkyu.tistory.com/102 [MangKyu's Diary:티스토리]
