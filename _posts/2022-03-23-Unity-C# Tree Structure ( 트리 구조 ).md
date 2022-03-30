---
layout: single
title: "[Conor] Unity C# 트리 구조 기초편 ( Basic Tree Structure Algorithm )"
description : "Tree Structure Baisc"
tags : [Algorithm]
comments : true
published : true
categories : Unity-Exercise TreeStructure C#
classes : wide

---

## ⊙ Tree Structure ( 트리 구조 )

![TreeSturcture](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-23/treeStructure.png?raw=true)

## ○ Tree-related term ( 트리 관련 용어 )

| Term ( 용어 )                              | Explain ( 설명 )                                             |
| ------------------------------------------ | ------------------------------------------------------------ |
| Parent node ( 부모 노드 )                  | A is the parent node of B ( A는 B의 부모 노드 입니다. )      |
| Child node ( 자식 노드 )                   | B is the child node of A ( B는 A의 자식 노드 입니다.)        |
| Sibling node ( 형제 노드 )                 | C is a sibling node to each other ( C는 서로 형제 노드이다. ) |
| Ancestor ( 선조 )                          | A is the ancestor of this tree. ( A는 선조 노드이다. )       |
| Descendant ( 자손 )                        | C is the descendant of this tree ( C는 자손 노드이다. )      |
| Root ( 루트 )                              | Root is the same as Ancestor ( 선조와 같습니다. )            |
| Leaf ( 잎 )                                | Leaf is the same as Descendant ( 자손과 같습니다. )          |
| Depth ( 노드의 깊이 )                      | From A to C, it is 2 depth ( A에서 B까지는 2뎁스 입니다. )   |
| Height ( 트리의 높이 )                     | Calculate the starting point as the inverse of the depth. ( 뎁스와 반대로 아래서 위로 계산합니다. ) |
| Subtree ( 트리의 재귀적 속성 및 서브트리 ) | Tree has recursive properties. ( 재귀적 속성을 지닙니다.)    |



## ○ Source TreeStructure

![SourceTreeStructure](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-23/SourceTreeStructure.png?raw=true)

## ○ Source Code ( 소스 코드 ) - C#

````c#
using System;
using System.Collections.Generic;

namespace Exercise
{
    class TreeNode<T>
    {
        public T Data { get; set; }
        public List<TreeNode<T>> Children { get; set; } = new List<TreeNode<T>>();
    }

    class Program
    {
        static TreeNode<string> MakeTree()
        {
            TreeNode<string> root = new TreeNode<string>() { Data = "CaptainKorea" };
            {
                {
                    TreeNode<string> node = new TreeNode<string>() { Data = "Conor" };
                    node.Children.Add(new TreeNode<string>() { Data = "Aono" });
                    node.Children.Add(new TreeNode<string>() { Data = "Bono" });
                    node.Children.Add(new TreeNode<string>() { Data = "Cono" });
                    root.Children.Add(node);
                }
                {
                    TreeNode<string> node = new TreeNode<string>() { Data = "Eonor" };
                    node.Children.Add(new TreeNode<string>() { Data = "Dono" });
                    node.Children.Add(new TreeNode<string>() { Data = "Eono" });
                    root.Children.Add(node);
                }
            }

            return root;
        }

        static void PrintTree( TreeNode<string> root )
        {
            // Access the Data ( 데이터에 접근 )
            Console.WriteLine(root.Data);

            foreach ( TreeNode<string> child in root.Children )
            {
                PrintTree(child);
            }
            /*
             * Result : 
                CaptainKorea
                Conor <--- First child Tree ( 첫번째 자식 트리 구조부터 출력됩니다. )
                Aono
                Bono
                Cono
                Eonor <--- Second child Tree
                Dono
                Eono
            */
        }

        // Let's find the height of the tree structure. ( 트리 구조의 높이를 구해봅시다. )
        static int GetHeight( TreeNode<string> root )
        {
            int height = 0;

            // Check each tree and return the highest height.( 트리 각각을 방문해서 가장 높은 높이를 반환하도록 합니다. )
            foreach ( TreeNode<string> child in root.Children )
            {
                int newHeight = GetHeight(child) + 1;
                if (height < newHeight) height = newHeight;
                // --> height = Math.Max(height, newHeight;  This is a high-quality code with visibility ( if문을 대체하는 고오오오~급진 코드입니다~ )
            }

            return height;
        }

        static void Main(string[] args)
        {
            TreeNode<string> root = MakeTree();
            PrintTree(root);
        }
    }
}
````

