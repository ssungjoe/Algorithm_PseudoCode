# 해시테이블
- 충돌해결 : 분리연쇄법
```pseudo
Alg findElement(k)
    input bucket array A[0..M-1] hash function h, key k
    output element with key k

1. v ← h(k)
2. return A[v].findElement(k)
```
```pseudo
Alg insertItem(k, e)
1. v ← h(k)
2. A[v].insertItem(k, e)
3. return
```
```pseudo
Alg removeElement(k)
1. v ← h(k)
2. return A[v].removeElement(k)
```
```pseudo
Alg initBuckeyArray()
    input bucket array A[0..M-1]
    output bucket array A[0..M-1] initialized with null buckets

1. for i ← 0 to M-1
       A[i] ← empty list
2. return
```
- 개방주소법 (탐색, 삽입)
```pseudo
Alg findElement(k)
    input bucket array A[0..M-1], hase function h, key k
    output element with key k

1. v ← h(k)
2. i ← 0
3. while (i < M)
       b ← getNextBucket(v, i)
       if (isEmpty(A[b]))
           return NoSuchKey
       elseif (k = key(A[b]))
           return element(A[b])
       else
           i ← i+1
4. return NoSuchKey
```
```pseudo
Alg insertItem(k, e)
1. v ← h(k)
2. i ← 0
3. while (i < M)
       b ← getNextBucket(v, i)
       if (isEmpty(A[b]))
           Set bucket A[b] to (k, e)
           return
       else
           i ← i+1
4. overflowException()
5. return
```
```pseudo
Alg getNextBucket(v, i)
1. return (v+i) % M             {linear probing}
```
```pseudo
Alg getNextBucket(v, i)
1. return (v+i²) % M            {quadratic probing}
```
```pseudo
Alg getNextBucket(v, i)
1. return (v+i*h'(k)) % M       {double hashing}
```
```pseudo
Alg initBucketArray()
    input bucket array A[0..M-1]
    output bucket array A[0..M-1] initialized with null buckets

1. for i ← 0 to M-1
       A[i].empty ← 1           {set bucket empty}
2. return
```
```pseudo
Alg isEmpty(b)
    input bucket b
    output boolean

1. return b.empty
```
