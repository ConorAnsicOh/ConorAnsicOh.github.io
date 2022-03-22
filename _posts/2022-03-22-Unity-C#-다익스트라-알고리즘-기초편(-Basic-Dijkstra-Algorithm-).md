---
layout: single
title: "Unity C# 다익스트라 알고리즘 기초편( Basic Dijkstra Algorithm )"
description : "Implementing Dijkstra Algorithm Using C# ( C#을 이용하여 다익스트라 알고리즘을 구현해보기 )"
tags : [C#]
comments : true
published : true
categories : Unity Exercise
classes : wide
---

⊙ Dijkstra Algorithm 다익스트라 알고리즘 익히기

​	Algorithm Route

![Dijkstra](https://github.com/ConorAnsicOh/conoransicoh.github.io/blob/master/_images/2022-03-22/BFS.png?raw=true)

​	Source

````c#
using System;
using System.Collections.Generic;

namespace Exercise
{
    class Graph
    {
        int[,] adj = new int[6, 6]
        {
            { -1, 15, -1, 35, -1, -1 },
            { 15, -1,05, 10, -1, -1 },
            { -1, 05, -1, -1, -1, -1 },
            { 35, 10, -1, -1, 05, -1 },
            { -1, -1, -1, 05, -1, 05 },
            { -1, -1, -1, -1, 05, -1 },
        };

        public void Dijkstra(int start)
        {
            bool[] visited = new bool[6];
            int[] distance = new int[6];
            int[] parent = new int[6];

            Array.Fill( distance, Int32.MaxValue); // just fill in array with huge num

            distance[start] = 0;
            parent[start] = start;

            while( true )
            {
                // Store the Ways and Numbers of the most likely candidates
                // 가장 유력한 후보의 거리와 번호를 저장한다.
                int closest = Int32.MaxValue;
                int now = -1;
                for ( int i = 0; i < 6; i++ )
                {
                    // Skip the peak you've already visited.
                    // 이미 방문한 정점은 스킵
                    if (visited[i]) continue;
					// Skip it if it has not yet been discovered or is farther than existing candidates
                    // 아직 발견 된 적이 없거나, 기존 후보보다 멀리 있으면 스킵
                    if (distance[i] == Int32.MaxValue || distance[i] >= closest) continue;
                    // Update information because it is the best candidate.
                    // 아래는 발견한 목표 후보중 가장 좋은 목표임을 의미하므로 정보를 갱신한다.
                    closest = distance[i];
                    now = i;
                }

                // There's no next candidate -> When all were cut off or the search was completed
                // 다음 후보가 하나도 없다 -> 모두 단절되었거나 마무리된 경우.
                if (now == -1) break;


				//Visite this candidate because it is the best candidate.
                //가장 좋은 후보를 찾았으니 방문한다.
                visited[now] = true;

                // The shortest distance found according to the situation is updated by examining the visited and adjacent candidates.
                //방문한 후보와 인접한 후보들을 조사해서 상황에 따라 발견한 최단거리를 갱신한다.
                for( int next = 0; next <6; next++)
                {
                    // Skip the Unconnected candidate
                    // 연결되지 않은 후보는 스킵
                    if (adj[now, next] == -1) continue;
                    // Skip the peak you've already visited.
                    // 이미 방문한 후보는 스킵
                    if (visited[next]) continue;

                    // Calculate the shortest distance for newly surveyed candidates
                    // 새로 조사된 후보의 최단거리를 계산한다.
                    int nextDist = distance[now] + adj[now, next];
                    // If the existing shortest distance found is greater than the newly investigated shortest distance, the information is refreshed.
                    // 기존의 발견한 최단거리가 새로 조사된 최단거리보다 크면 정보를 갠신한다.
                    if ( nextDist < distance[next])
                    {
                        distance[next] = nextDist;
                        parent[next] = now;
                    }
                }
            }
        } 
    }

    class Program
    {
        static void Main(string[] args)
        {
            Graph graph = new Graph();
            graph.Dijkstra(0);
        }
    }
}

````

