# 이진탐색트리
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
- 삭제
```pseudo
Alg removeElement(k)
    input binary seach tree t, key k
    output element with key k

1. w ← trereSearch(root(), k)
2. if (isExternal(w))
       return NoSuchKey
3. e ← element(w)
4. z ← leftChild(w)
5. if (!isExternal(z))
       z ← rightChild(w)
6. if (isExternal(z))               {case 1}
       reduceExternal(z)
   else                             {case 2}
       y ← inOrderSucc(w)
       z ← leftChild(y)
       Set node w to (key(y), element(y))
       reduceExternal(z)
7. return e
```

<br>

# AVL 트리
- 삽입
```pseudo
Alg insertItem(k ,e)
    input AVL tree T, key k, element e
    output none

1. w ← treeSearch(root(), k)
2. if (isInternal(w))
       return
   else
       Set node w to (k, e)
       expandExternal(w)
       searchAndFixAfterInsertion(w)
       return
```
```pseudo
Alg searchAndFixAfterInsertion(w)
    input internal node w
    output none

1. w에서 T의 루트를 향해 올라가다 처음 만나는 불균형 노드를 z라 하자    {만일 그런 z가 없다면 return}
2. z의 높은 자식을 y라 하자                                          {y는 w의 조상이 됨}
3. y의 높은 자식을 x라 하자                                          {x가 w랑 일치할 수도 있고, x가 z의 손자이다}
4. restructure(x, y, z)                                             {b를 루트로하는 모든 노드는 균형 유지, 높이 균형 속성이 노드 x, y, z에서 모두 복구}
5. return
```
```pseudo
Alg restructure(x, y, z)
    input a node x of a binary search tree T that has both a parent y and a grandparent z
    output tree T after restructuring in involving nodes x, y and z

1. x, y, z의 중위순회 방문순서의 나열을 (a, b, c)라 하자
2. x, y, z의 부트리들 가운데 x, y, z가 루트인 부트리를 제외한 나머지 4개의 부트리들의 중위순회 방문순서 나열을 (T_0, T_1, T_2, T_3)이라 하자
3. z를 루트로 하는 부트리를 b를 루트로 하는 부트리로 대체
4. T_0와 T_1을 각각 a의 왼쪽, 오른쪽 부트리로 만듦
5. T_2와 T_4를 각각 c의 왼쪽, 오른쪽 부트리로 만듦
6. a와 c를 각각 b의 왼쪽, 오른쪽 자식으로 만듦
7. return b
```
- 삭제
```pseudo
Alg removeElement(k)
    input AVL tree T, key k
    output element with key k

1. w ← treeSearch(root(), k)
2. if (isExternal(w))
       return NoSuchKey
3. e ← element(w)
4. z ← leftChild(w)
5. if (!isExternal(z))
       z ← rightChild(w)
6. if (isExternal(z))
       zs ← reduceExternal(z)
   else
       y ← inOrderSucc(w)
       z ← leftChild(y)
       Set node w to (key(y), element(y))
       zs ← reduceExternal(z)
7. searchAndFixAfterRemoval(parent(zs))
8. return e
```
```pseudo
Alg searchAndFixAfterRemoval(w)
    input internal node w
    output none

1. w에서 T의 루트로 올라가다 처음 만나는 불균형 노드를 z라 하자         {그런 z가 없으면 return}
2. z의 높은 자식을 y라 하자
3. y의 두 자식 중 높은 자식을 x라 하고, 만약 두 자식의 높이가 같으면 둘 중 y와 같은 쪽의 자식을 x로 택함
4. b ← restructure(x, y, z)                                         {변수 b를 루트로 하는 부트리에서 균형 속성 지역적으로 복구됨, 그러나 b의 조상이 균형을 잃을 수도 있음}
5. T를 b의 부모부터 루트까지 올라가면서 불균형인 노드를 찾아 복구하길 반복
```

<br>

# 스플레이 트리
- 트리의 노드가 탐색 또는 갱신을 위해 접근된 후 플레이되는 이진 탐색 트리
```pseudo
Alg splay(x) : O(h) {h는 스플레이 트리의 높이}
    input internal node x
    output none

1. if (isRoot(x))
       return
2. if (isRoot(parent(x)))                       {zig}
       if(x = leftChild(root()))
           rightRotate(x, root())
       else
           leftRotate(x, root())
       return
3. p ← parent(x)
4. g ← parent(p)
5. if (x = leftChild(leftChiild(g)))            {zig-zig}
       rightRotate(p, g)
       rightRotate(x, p)
   elseif (x = rightChild(rightChild(g)))       {zig-zig}
       leftRotate(p, g)
       leftRotate(x, p)
   elseif (x = leftChild(rightChild(g)))        {zig-zag}
       rightRotate(x, p)
       leftRotate(x, g)
   else         {x = rightChild(leftChild(g))}  {zig-zag}
       leftRotate(x, p)
       rightRotate(x, g)
6. splay(x)
```