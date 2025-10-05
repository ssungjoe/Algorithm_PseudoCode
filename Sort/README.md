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

<br>

# 힙
- 힙에 삽입
```pseudo
Alg insertItem(k)
    input key k, node last
    output none

1. advanceLast()        {새로운 마지막 노드 찾기}
2. z ← last
3. Set node z to k
4. expandExternal(z)    {z(=k)를 내부노드로 확장}
5. upHeap(z)            {힙순서 속성 복구}
6. return
```
```pseudo
Alg upHeap(v)
    input node v
    output none

1. if (isRoot(v))
       return
2. if (key(v) ≥ key(parent(v)))     {최소힙}
       return
3. swapElements(v, parent(v))
4. upHeap(parent(v))                {재귀}
```
```pseudo
Alg expandExternal(z)
    input external node z
    output none

1. l ← getnode()
2. r ← getnode()
3. l.left ← ∅       {빈 노드 l 생성, 부모를 z로 지정}
4. l.right ← ∅
5. l.parent ← z
6. r.left ← ∅       {빈 노드 r 생성, 부모를 z로 지정}
7. r.right ← ∅
8. r.parent ← z
9. z.left ← l        {z의 왼쪽 오른쪽 자식 최신화}
10. z.right ← l
11. return
```
- 힙에서 삭제
  + removeMin은 힙으로부터 루트 키를 삭제
```pseudo
Alg removeMin()
    input node last
    output key

1. k ← key(root())          {k는 원래 루트값}
2. w ← last
3. Set root to key(w)       {w(=last)를 root로 설정}
4. retreatLast()            {last를 하나 왼쪽 노드로 갱신}
5. z ← rightChild(w)
6. reduceExternal(z)        {w와 그 자식들을 leaf node로 축소}
7. downHeap(root())         {힙속성 복구}
8. return k
```
```pseudo
Alg downHeap(v)
    input node v whose left and right subtrees are heaps
    output a heap with root v

1. if (isExternal(leftChild(v)) & isExternal(rightChild(v)))
       return
2. smaller ← leftChild(v)
3. if (isInternal(rightChild(v)))
       if (key(rightChild(v)) < key(smaller))
           smaller ← rightChild(v)
4. if (key(v) ≤ key(smaller))
       return
5. swapElements(v, smaller)
6. downHeap(smaller)
```
```pseudo
Alg reduceExternal(z)
    input external node z
    output the node replacing the parent node of the removed node z

1. w ← z.parent
2. zs ← sibiling(z)
3. if (isRoot(w))
       root ← zs
       zs.parent ← ∅
   else
       g ← w.parent
       zs.parent ← g
       if (w = g.left)
           g.left ← zs
       else             {w = g.right}
           g.right ← zs
4. putnode(z)
5. putnode(w)
6. return zs
```