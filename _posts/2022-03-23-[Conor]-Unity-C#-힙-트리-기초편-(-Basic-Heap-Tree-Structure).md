---
layout: single
title: "[Conor] Unity C# 힙 트리 기초편 ( Basic Heap Tree Structure)"
description : "Heap Tree Structure"
tags : [Algorithm]
comments : true
published : true
categories : Unity-Exercise Binary TreeStructure
classes : wide
---



## ⊙Binary Tree Structure ( 이진 트리 )

![Binary TreeSturcture](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-23/BinaryTree.png?raw=true)

## ⊙Heap Tree Structure ( 힙 트리 )

![Heap TreeStructure](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-23/HeapTree.png?raw=true)

### ○The Way of ( 구성하는 방법 ).

· Condition 1 : The value fo the parent node should always be greater than the value of the child node.

( 조건 1 : 부모 노드가 가진 값은 항상 자식 노드가 가진 값보다 커야한다. )

· Condition 2 : Additional nodes must be filled from the left side of the last level node.

( 건 2 : 추가 되는 노드는 마지막 레벨 노드의 왼쪽부터 채워야한다. )

· Charactoristics 1 : If you know the number of nodes, you can unconditionally determine the tree structure.

특징 1 : 노드의 개수를 알면 트리 구조는 무조건 확정 할 수 있다.

````c#
// function example. ( 공식 예시 )
int[] heap = new int[5]; // If you create five nodes. ( 5개 노드의 트리를 만들었다면~ )
// The left child node 'i' is (2*i)+1. ( i번 노드의 왼쪽 자식은 (2 * i) + 1 번째다. )
// The right child node 'i' is (2*i)+2. ( i번 노드의 오른쪽 자식은 (2 * i) + 2 번째다. )
// The parent of node 'i' is (i-1)/2. ( i번 노드의 부모는 (i - 1) / 2 번째다. )
````

· Condition 3 : The newly added node switches its location with the parent when the newly added node is larger than the parent.

조건 3 : 새롭게 추가된 노드는 부모와 비교하여 새롭게 추가된 노드가 더 큰 경우 부모와 위치를 바꾼다.

### ○ Logic order when parent node is removed. ( 상위 노드를 제거한 경우 로직 순서. )

Order 1 : Move the finally added node to the removed node location.

순서 1 : 최종 추가되었던 노드를 제거된 곳으로 옮겨온다.

Order 2 : The moved node descends according to its location by comparing to the left child.

순서 2 : 옮겨온 노드는 왼쪽 자식과 비교하여 부터 비교하여 위치에 맞게 내려간다.



