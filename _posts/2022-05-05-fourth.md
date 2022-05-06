---
layout: single
title:  "정렬 "
---

# 정렬 알고리즘
- 선택 정렬
- 버블 정렬
- 삽입 정렬
- 퀵 정렬
- 힙 정렬
- 쉘 정렬

* 2의 5제곱 ~ 2의 20제곱

# 선택정렬


선택정렬은 앞에서부터 차례대로 정렬하는 방법이다.

먼저 주어진 리스트 중에 최소값을 찾고 그 값을 맨 앞에 위치한 값과 교체하는 방식으로 진행하는 정렬방법이다.  

코드가 직관적이기에 구현도 비교적 간단하다.  

내림차순으로 정렬되어 있는 자료를 오름차순으로 재정렬할 때 최적의 효율을 보여주지만 이미 정렬된 상태에서 소수의 자료가 추가됨으로 재정렬하게 되는 때에는 최악의 처리 속도를 보여준다는 단점이 있다.

<br/>

```c
void selection_sort(int list[], int n)
{
    int i,j,least,tmp;
    
    printf("선택 정렬 중... ");
    for(i=0; i<n-1; i++)
    {
        least=i;
        for(j=i+1; j<n; j++)
            if(list[j]<list[least]) least=j;
        SWAP(list[i], list[least], tmp);
    }
}
```
# 버블정렬

버블정렬은 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 끝부터 정렬하는 방식을 말한다.

마찬가지로 코드가 간단하므로 구현이 간편하다.  

데이터를 하나씩 비교할 수 있어서 정밀하게 비교가 가능하나 비교횟수가 많아지므로 성능면에서는 좋지 않다.  

첫 번째 원소부터 마지막 원소까지 반복하여 한 단계가 끝나면 가장 큰 원소를 마지막 자리로 정렬하는 식으로 정렬이 된다. 

<br/>

```c
void bubble_sort(int list[], int n)
{
    int i, j, tmp;
    printf("버블 정렬 중... ");
    for(i=n-1; i>0; i--)
    {
        for(j=0; j<i; j++)
            if(list[j]>list[j+1])
                SWAP(list[j], list[j+1], tmp);
    }
}
```
# 삽입정렬
삽입 정렬은 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 정렬 방법이다.  

버블정렬은 비교대상의 메모리 값이 정렬되어 있음에도 불구하고 비교연산을 하는 부분이 있는데 삽입정렬은 기본적으로 버블정렬의 비교횟수를 줄이고 크기가 적은 데이터 집합을 정렬하는 루팅을 작성할 시 버블정렬보다 탁월한 성능 효율을 보여준다.

<br/>

```c
void insertion_sort(int list[], int n)
{
    int i, j, key;
    printf("삽입 정렬 중... ");
    for(i=1; i<n; i++)
    {
        key=list[i];
        for(j=i-1; j>=0 && list[j]>key; j--)
            list[j+1]=list[j];
        list[j+1]=key;
    }
}
```
# 퀵정렬
연속적인 분할에 의한 정렬방식이다.  

처음 하나의 축을 먼저 정하여 이 축의 값보다 작은 값은 왼쪽에 큰 값은 오른쪽으로 위치시킨뒤 왼쪽과 오른쪽의 수 들은 다시 각각의 축으로 나누어져 축값이 1이 될 때까지 정렬다. 가장 많이 사용되는 정렬법이나 안정성이 떨어진다는 단점이 있다. 

<br/>

```c
int partition(int list[], int left, int right)
{
    int pivot=list[left], tmp, low=left, high=right+1;
 
    do{
        do
        low++;
        while(low<=right && list[low]<pivot);
 
        do
        high--;
        while(high>=left && list[high]>pivot);
        if(low<high) SWAP(list[low], list[high], tmp);
    }while(low<high);
 
    SWAP(list[left], list[high], tmp);
    return high;
}
void quick_sort(int list[], int left, int right)
{
    if(left<right)
    {
        int q=partition(list, left, right);
        quick_sort(list, left, q-1);
        quick_sort(list, q+1, right);
    }
}
```
# 힙정렬
힙 정렬은 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법이다. 

시간복잡도가 O인 정렬 알고리즘 중에서는 부가적인 메모리가 전혀 필요없다는 게 큰 장점인 정렬 방식이다.

<br/>

```c
void insert_max_heap(element item, int *n) 
{
       int i;
       if(HEAP_FULL(*n)) {
            fprintf(stderr,”The heap is full. ₩n”);
      exit(1);
     }
      i = ++(*n);
    while((i!=1)&&(item.key>heap[i/2].key)) { 
     heap[i] = heap[i/2];
      i /= 2;
   }
      heap[i] = item;
}
```
# 쉘정렬
알고리즘이 간단하여 프로그램으로 쉽게 구현할 수 있다.  

멀리 있는 레코드들끼리 비교 및 교환될 수 있으므로, 어떤 데이터가 제 위치에서 멀리 떨어져 있다면 여러 번의 교환이 발생하는 버블정렬 방식의 단점을 해결할 수 있다.

<br/>

```c
void inc_insertion_sort(int list[], int first, int last, int gap)
{
    int i, j, key;
    for(i=first+gap; i<=last; i=i+gap)
    {
        key=list[i];
        for(j=i-gap; j>=first && key<list[j]; j=j-gap)
            list[j+gap]=list[j];
        list[j+gap]=key;
    }
}
void shell_sort(int list[], int n)
{
    int i, gap;
    printf("쉘 정렬 중... ");
    for(gap=n/2; gap>0; gap=gap/2)
    {
        if((gap%2)==0) gap++;
        for(i=0; i<gap; i++)
            inc_insertion_sort(list, i, n-1, gap);
    }
}
```

- 원본 배열을 복사하는 함수

```c
void CopyArr(void)
{
    int i;
    for(i=0; i<n; i++)
        list[i]=original[i];
}
```

- 실행 시간을 측정 및 출력하는 함수

```c
void CalcTime(void)
{
    used_time=finish-start;
    printf("완료!\n소요 시간 : %f sec\n\n",(float)used_time/CLOCKS_PER_SEC);
}
 
 
void main ()
{
    int i;
    
    n=MAX_SIZE;
    for(i=0; i<n; i++)
        original[i]=rand();
    
    printf("데이터의 개수 : %d\n\n", n);
 
    CopyArr();
    start=clock();
    printf("선택 정렬 중... ");
    selection_sort(list, n);
    finish=clock();
    CalcTime();
    
    CopyArr();
    start=clock();
    printf("힙 정렬 중... ");
    Heap_sort(list, n);
    finish=clock();
    CalcTime();
 
    CopyArr();
    start=clock();
    printf("버블 정렬 중... ");
    bubble_sort(list, n);
    finish=clock();
    CalcTime();
 
    CopyArr();
    start=clock();
    printf("쉘 정렬 중... ");
    shell_sort(list, n);
    finish=clock();
    CalcTime();
 
    CopyArr();
    start=clock();
    printf("합병 정렬 중... ");
    merge_sort(list, 0, n);
    finish=clock();
    CalcTime();
 
    CopyArr();
    start=clock();
    printf("퀵 정렬 중... ");
    quick_sort(list, 0, n);
    finish=clock();
    CalcTime();
}
```
