# 정렬

## 공부했던 블로그 적음 걍

솔직히 https://gmlwjd9405.github.io/ 여기 이 분 블로그 밖에 없음 그냥 정렬 공부할 때는 이 분 블로그가 최고인듯

## 안정 정렬, 불안정 정렬

- https://velog.io/@good159897/%EC%95%88%EC%A0%95-%EC%A0%95%EB%A0%AC-VS-%EB%B6%88%EC%95%88%EC%A0%95-%EC%A0%95%EB%A0%AC-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9D%B8%ED%84%B0%EB%B7%B0

- 여기 참고함

- **안정 정렬**과 **불안정 정렬**을 나누는 기준은 정렬할 배열에 중복된 값이 순서대로 정렬되느냐, 무작위로 섞이냐이다

- 값에 데이터가 하나의 정보만을 뜻하는 경우에는 상관이 없겠지만, 대부분의 자료에는 한 행에 여려가지 열이 있듯이 여러가지 데이터가 있기에 한 가지 열에 대해 불안정 정렬이 된다면 원하던 모습이랑은 다른 리스트의 정렬 상태를 마주할 수도 있다.

- 안정 정렬

1. 삽입 정렬
2. 버블 정렬
3. 병합 정렬

- 불안정 정렬

1. 선택 정렬
2. 퀵 정렬
3. 힙 정렬

## Shell Sort (셸 정렬)

- 삽입정렬을 보완한 알고리즘

- 조금 재밌는 알고리즘

- 코드 (아래 블로그에서 만든거 퍼온 거임)

- https://gmlwjd9405.github.io/2018/05/08/algorithm-shell-sort.html

```c
# include <stdio.h>
# define MAX_SIZE 10

// gap만큼 떨어진 요소들을 삽입 정렬
// 정렬의 범위는 first에서 last까지
void inc_insertion_sort(int list[], int first, int last, int gap){
  int i, j, key;

  for(i=first+gap; i<=last; i=i+gap){
    key = list[i]; // 현재 삽입될 숫자인 i번째 정수를 key 변수로 복사

    // 현재 정렬된 배열은 i-gap까지이므로 i-gap번째부터 역순으로 조사한다.
    // j 값은 first 이상이어야 하고
    // key 값보다 정렬된 배열에 있는 값이 크면 j번째를 j+gap번째로 이동
    for(j=i-gap; j>=first && list[j]>key; j=j-gap){
      list[j+gap] = list[j]; // 레코드를 gap만큼 오른쪽으로 이동
    }

    list[j+gap] = key;
  }
}

// 셸 정렬
void shell_sort(int list[], int n){
  int i, gap;

  for(gap=n/2; gap>0; gap=gap/2){
    if((gap%2) == 0)(
      gap++; // gap을 홀수로 만든다.
    )

    // 부분 리스트의 개수는 gap과 같다.
    for(i=0; i<gap; i++){
      // 부분 리스트에 대한 삽입 정렬 수행
      inc_insertion_sort(list, i, n-1, gap);
    }
  }
}

void main(){
  int i;
  int n = MAX_SIZE;
  int list[n] = {10, 8, 6, 20, 4, 3, 22, 1, 0, 15, 16};

  // 셸 정렬 수행
  shell_sort(list, n);

  // 정렬 결과 출력
  for(i=0; i<n; i++){
    printf("%d\n", list[i]);
  }
}
https://gmlwjd9405.github.io/2018/05/08/algorithm-shell-sort.html
```

## Quick Sort (퀵 정렬)

- 불안정 정렬, 비교 정렬

- 분할 정복 알고리즘, 평균적으로 **매우 빠른 수행 속도**를 자랑하는 방법

- 합병정렬과는 다르게 **비균등하게** 분할한다

- 순서

분할, 정복, 결합

1. 리스트 안에 한 요소를 선택하고, 이렇게 고른 원소를 **피벗(pivot)**이라고함
2. 피벗보다 작은 값을 왼쪽으로 큰 값을 오른쪽으로 옮김
3. 피벗을 제외한 왼쪽 오른쪽 값을 **순환 호출**하여 정렬을 반복, 부분 리스트를에서도 피벗을 정하고 피벗을 기준으로 2개의 리스트를 나누는 과정 반복
4. 3.을 리스트의 크기가 0또는 1이 될 때까지 반복

- 확실히 합병 정렬이랑 비슷하다 사촌 정도쯤 되는 것 같다

- 가장 빠른 속도를 보여주지만, 최악의 경우에는 $n^2$으로 극과 극인듯 하다.

- 코드는 알아서 블로그 가서 보자

- https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html

## 힙 정렬

- https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html

- 이거 보면 이해 ㅆㄱㄴ

- 자료구조 힙 알면 끝임 걍

----

분할 정렬은 알고 있어서 안씀