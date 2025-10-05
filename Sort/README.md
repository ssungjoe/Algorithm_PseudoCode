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

- 힙 정렬
```pseudo
Alg heapSort(L)
    input list L
    output sorted list L

1. H ← empty heap
2. while (!L.isEmpty)           {1기}
       k ← L.removeFirst()
       H.insertItem(K)
3. while (!H.isEmpty)           {2기}
       k ← H.removeMin()
       L.addLast(k)
4. return
```

- 제자리 힙 정렬
  + 최대힙을 사용해 구현한다
```pseudo
Alg inPlaceHeapSort(A)
    input array A of n keys
    output sorted array A

1. builHeap(A)
2. for i ← n downto 2
       A[1] ↔ A[i]
       downHeap(1, i-1)
3. return
```
```pseudo
Alg buildHeap(A)
    input array A of n keys
    output heap A of size n

1. for i ← 1 to n
       insertItem(A[i])
2. return
```
```pseudo
Alg downHeap(i, last)
    input index i of array A representing a maxheap of size last
    output none

1. left ← 2i
2. right ← 2i + 1
3. if (left > last)         {외부노드}
       return
4. greater ← left
5. if (right ≤ last)
       if (key(A[right]) > key(A[greater]))
           greater ← right
6. if (key(A[i]) ≥ key(A[greater]))
       return
7. A[i] ↔ A[greater]
8. downHeap(greater, last)
```

- 상향식 힙 생성 (재귀)
```pseudo
Alg buildHeap(L)
    input list L storing n keys
    output heap T storing the keys in L

1. T ← convertToCompleteBinaryTree(L)
2. rBuilHeap(v)
3. return T
```
```pseudo
Alg rBuildHeap(v)
    input node v
    output a heap with root v

1. if (isInternal(v))
       rBuildHeap(leftChild(v))
       rBuildHeap(rightChild(v))
       downHeap(v)
2. return
```
- 비재귀적 상향식 힙 생성
```pseudo
Alg buildHeap(A)
    input array A of n keys
    output heap A of size n

1. for i ← ⌊ n/2 ⌋ downto 1
    downHeap(i, n)
2. return
```

<br>

# 합병정렬
```pseudo
Alg mergeSort(L)
    input list L with n elements
    output sorted list L

1. if (L.size() > 1)
       L₁, L₂ ← partition(L, n/2)       {분할}
       mergeSort(L₁)                    {재귀}
       mergeSort(L₂)
       L ← merge(L₁, L₂)                {통치}
2. return

```
- 합병
```pseudo
Alg merge(L₁, L₂)
    input sorted list L₁ and L₂ with n/2 elements each
    output sorted list of L₁∪L₂

1. L ← empty list
2. whlie (!L₁.isEmpty() & !L₂.isEmpty())
       if (L₁.get(1) ≤ L₂.get(1))
           L.addLast(L₁.removeFirst())
       else
           L.addLast(L₂.removeFirst())
3. while (!L₁.isEmpty())
       L.addLast(L₁.removeFirst())
4. while (!L₂.isEmpty())
       L.addLast(L₂.removeFirst())
5. return L
```

<br>

# 퀵 정렬
```pseudo
Alg quickSort(L)
    input list L with n elements
    output sorted list L

1. if (L.size() > 1)
       k ← a position in L
       LT, EQ, GT ← partition(L, k)         {분할}
       quickSort(LT)                        {재귀}
       quickSort(GT)
       L ← merge(LT, EQ, GT)                {통치}
2. return
```
- 분할
```pseudo
Alg partition(L, k)
    input list L with n elements, position k of pivot
    output sublists LT, EQ, GT of the elements of L, less than, equal to, or greater than pivot, resp.

1. p ← L.get(k)                 {pivot}
2. LT, EQ, GT ← empty list
3. while (!L.isEmpty())
       e ← L.removeFirst()
       if (e < p)
           LT.addLast(e)
       elseif (e = p)
           EQ.addLast(e)
       else                     {e > p}
           GT.addLast(e)
5. return LT, EQ, GT
```