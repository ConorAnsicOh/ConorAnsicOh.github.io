---
layout: single
title: "[Conor] Unity C# BFS 기초편(Basic BFS Algorithm)"
description : "Simple implementation of BFS, one of the path finding logics. (길찾기 로직중 하나인 BFS를 간단히 구현해보기)"
tags : [Algorithm]
comments : true
published : true
categories : Unity-Exercise BFS Algorithm C#
classes : wide
---



**⊙ BFS ( Breadth First Search ) 너비 우선 탐색 기법**

​	Algorithm Route

![BFS](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-22/BFS.png?raw=true)

​	Source

```` C#
using System;
using System.Collections.Generic;

namespace Exercise
{
    class Graph
    {
        int[,] adj = new int[6, 6]
        {
            { 0, 1, 0, 1, 0, 0 },
            { 1, 0, 1, 1, 0, 0 },
            { 0, 1, 0, 0, 0, 0 },
            { 1, 1, 0, 0, 1, 0 },
            { 0, 0, 0, 1, 0, 1 },
            { 0, 0, 0, 0, 1, 0 },
        };

        List<int>[] adj2 = new List<int>[]
        {
            new List<int>() { 1, 3 },
            new List<int>() { 0, 2, 3},
            new List<int>() { 1 },
            new List<int>() { 0, 1, 4},
            new List<int>() { 3, 5 },
            new List<int>() { 4 },
        };

        public void BFS( int start )
        {
            bool[] found = new bool[6];
            int[] parent = new int[6];
            int[] distance = new int[6];

            // FIFO is an important thing in BFS so use Queue as FIFO. 
            // 선입선출을 위해 스택이 아닌 큐를 씁니다.
            Queue<int> q = new Queue<int>();
            q.Enqueue(start);
            found[start] = true;
            parent[start] = start;
            distance[start] = 0;

            while( q.Count > 0 )
            {
                int now = q.Dequeue();
                Console.WriteLine(now);

                for ( int next = 0; next < 6; next++ )
                {
                    if ( adj[now, next] == 0 ) // 인접하지 않으면 스킵
                    {
                        continue;
                    }
                    if (found[next])  // 이미 발견한 것이면 스킵
                    {
                        continue;
                    }

                    q.Enqueue(next);
                    parent[next] = now; // Result : {0, 0, 1, 0, 3, 4}
                    distance[next] = distance[now] + 1; // Result : {0, 1, 2, 1, 2, 3}
                    found[next] = true; // Result : { true,true,true,true,true,true }
                }
            }
        }
       
    }

    class Program
    {
        static void Main(string[] args)
        {
            // DFS ( Depth First Search 깊이 우선 탐색 )
            // BFS ( Breadth First Search 너비 우선 탐색 )

            Graph graph = new Graph();
            graph.BFS(0);
        }
    }
}

````
