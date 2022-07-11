# Algorithm: non-Comparison Sort

## Counting Sort

말 그대로 몇 개인지 개수를 세어 정렬하는 방식이다.

1. 정렬하고자 하는 원소 값 중 최댓값을 크기로 갖는 임시 배열을 만든다. 

2. 임시 배열엔 index 에 해당하는 원소 값들의 갯수를 저장한다. ( `temp_arr[4]` 엔 `4` 의  갯수를 저장한다. )  

3. 임시 배열의 요소들이 누적합을 가지도록 변경한다. 

4. 최종 결과를 담을 배열을 생성하고, 임시 배열의 원소에 해당하는 인덱스에 값을 넣어준다. 

   `temp_arr[4]` 의 값이 11이라면, `sorted_arr[11]` 에 `4`를 넣고, `temp_arr[4]` 의 값을 1 감소시킨다. 

>[Counting Sort](https://www.cs.usfca.edu/~galles/visualization/CountingSort.html)

```java
int arr[5]; 		// [5, 4, 3, 2, 1]
int sorted_arr[5];

// 과정 1 - counting 배열의 사이즈를 최대값 5가 담기도록 크게 잡기
int counting[6];	// 단점 : counting 배열의 사이즈의 범위를 가능한 값의 범위만큼 크게 잡아야 하므로, 비효율적이 됨.

// 과정 2 - counting 배열의 값을 증가해주기.
for (int i = 0; i < arr.length; i++) {
    counting[arr[i]]++;
}
// 과정 3 - counting 배열을 누적합으로 만들어주기.
for (int i = 1; i < arr.length; i++) {
    counting[i] += counting[i - 1];
}
// 과정 4 - 뒤에서부터 배열을 돌면서, 해당하는 값의 인덱스에 값을 넣어주기.
for (int i = arr.length - 1; i >= 0; i--) {
    sorted_arr[counting[arr[i]]] = arr[i];
    counting[arr[i]]--;
}
```

시간 복잡도 `O(n)`, 정확하게는 `O(n + k)`, 공간 복잡도 `O(n)`

## Radix Sort 

입력 데이터의 최댓값 증가에 의한 Counting Sort 의 비효율성을 개선.

단 정렬하고자 하는 데이터의 길이가 모두 동일해야 한다. 

>https://lktprogrammer.tistory.com/48

```java
void radixsort(int arr[], int n) {
     // 최댓값 자리만큼 돌기
    int m = getMax(arr, n);
    
    // 최댓값을 나눴을 때, 0이 나오면 모든 숫자가 exp의 아래
    for (int exp = 1; m / exp > 0; exp *= 10) {
        countSort(arr, n, exp);
    }
}
```

시간 복잡도 `O(d * (n + k))`, d 는 자릿수, k 는 10으로 고정.