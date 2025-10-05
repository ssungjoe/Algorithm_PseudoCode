# 우선순위 큐
- PQ-Sort
  + L의 원소를 차례로 삭제해 우선순위 큐 P에 삽입
  + P의 원소를 최소 키 순으로 삭제해 L에 다시 삽입 
```pseudo
Alg PQ-Sort(L)
    input list L
    output sorted list L

1. P
2. while (!L.isEmpty())
       e  ← L.removeFirst()
       P.insertItem(e)
3. while (!P.isEmpty())
       e ← P.removeMin()
       L.addLast(e)
4. return    
```
- 제자리 선택 정렬
  + 다음은 입력이 배열임을 전제로 함
```pseudo
Alg inPlaceSelectionSort(A)
    input array A of n keys
    output sorted array A

1. for pass ← 0 to n-2
       minLoc ← pass
       for j ← (pass+1) to n-1
           if (A[j] < A[minLoc])
               minLoc ← j
       A[pass] ↔ A[minLoc]
2. return
```
- 제자리 삽입 정렬
  + 입력이 배열임을 전제로 함
```pseudo
Alg inPlaceInsertionSort(A)
    input array A of n keys
    output sorted array A

1. for pass ← 1 to n-1
       save ← A[pass]
       j ← pass-1
       while ((j≥0) & (A[j]>save))
           A[j+1] ← A[j]
           j ← j-1
       A[j+1] ← save
2. return
```