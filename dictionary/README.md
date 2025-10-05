# 사전
- 선형탐색
```pseudo
Alg findElement(k) : O(n)
    input list L, key k
    output element with key k

1. L.initialize(i)
2. while (L.isValid(i))             {위치 i가 리스트 L의 적법한 위치인지 확인}
       if (L.key(i) = k)
           return L.element(i)
       else
           L.advance(i)
3. return NoSuchKey
```
- 선형탐색 (순서리스트 사전 ver.)
```pseudo
Alg findElement(k) : O(n)
    input list L, key k
    output element with key k

1. L.initialize(i)
2. while (L.isValid(i))
       if (L.key(i) = k)
           return L.element(i)
       elseif (L.key(i) > k)
           return NoSuchKey
       else
           L.advance(i)
3. return NoSuchKey
```
- 이진탐색
```pseudo
Alg findElement(k) : O(log n)
    input sorted array A[0..n-1], key k
    output element with key k

1. return rFindElement(k, 0, n-1)
```
```pseudo
Alg rFindElement(k, l, r)
1. if (l > r)
    return NoSuchKey
2. mid ← (l + r)/2
3. if (k = key(A[mid]))
       return element(A[mid])
   elseif (k < key(A[mid]))
       return rFindElement(k, l, mid-1)
   else                                     {k > key(A[mid])}
       return rFindElement(k, mid+1, r)
```
- 탐색
```pseudo
Alg findElement(k)
    input binary search tree T, key k
    output element with key k

1. w ← treeSearch(root(), k)
2. if (isExternal(w))
       return NoSuchKey
   else
       return element(w)
```
```pseudo
Alg treeSearch(v, k)
    input node v of a binary search tree, key k
    output node w, s.t. either w is an internal node storing key k or w is the external node where key k would belong if it existed

1. if (isExternal(v))
       return v
2. if (k = key(v))
       return v
   elseif (k < key(v))
       return treeSearch(leftChild(v), k)
   else                                     {k > key(v)}
       return treeSearch(rightChild(v), k)
```
- 삽입
```pseudo
Alg insertItem(k, e)
    input binary search tree T, key k, element e
    output none

1. w ← treeSearch(root(), k)
2. if (isInternal(w))
       return
   else
       Set node w to (k, e)
       expandExternal(w)
       return
```