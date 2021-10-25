---
title: Graph-Traverse
date: 2021-10-23 15:29:52
tags: 数据结构
---

**图的遍历**

>图的遍历：从图的某一顶点出发访问图中的所有顶点，并且每个顶点只访问一次

- **深度优先搜索（DFS）**
>首先访问图中某一顶点，以该顶点v0为出发点
>任选一个与顶点邻接的未被访问的顶点v1，访问v1
>以v1为新的出发点继续进行搜索，直到图中所有顶点均被访问到

用一个visited数组来存储顶点是否被访问过

- **以下是用邻接矩阵实现DFS的过程**

        #include<bits/stdc++.h>
        #define MAX_NUM 100
        using namespace std;
        //定义访问数组 
        bool visited[MAX_NUM];
        //定义邻接矩阵 
        typedef struct Arc { 
            int adj;
        }Arc, AdjMatrix[MAX_NUM][MAX_NUM];

        typedef struct {
            char vex[MAX_NUM];
            AdjMatrix arcs;
            int vexnum, arcnum;
        }Graph;

        //用邻接矩阵实现DFS 
        void DFSTraverse(Graph g,int v) {
            visited[v] = true;
            cout << g.vex[v];
            for(int j=0;j<g.vexnum;j++){
                if(!visited[j] && g.arcs[v][j].adj!=0)
                    DFSTraverse_1(g,j);
            }
            
        }

        void initGraph(Graph &g){
            cout<< "请输入顶点数 边数"; 
            cin>> g.vexnum >> g.arcnum;
            cout<< "请依次输入各个顶点的编号";
            for(int i=0;i<g.vexnum;i++){
                cin>> g.vex[i];
            }
            cout<< "输入边矩阵";
            for(int i=0;i<g.vexnum;i++){
                for(int j=0;j<g.vexnum;j++){
                    cin>> g.arcs[i][j].adj;
                }
            }
        }
        int main(){
            Graph g;
            initGraph(g);
            for(int i=0;i<g.vexnum;i++){
                visited[i] = false;
            }
            DFSTraverse(g,0);
        }

- **以下是使用邻接表实现的DFS**

        #include<stdio.h>
        #include<iostream>
        #include<stdlib.h>
        #define MAX_NUM 100
        using namespace std;

        //定义访问数组 
        bool visited[MAX_NUM];
        //定义邻接表 
        typedef struct ArcNode {
            int adjvex;//指向顶点 
            struct ArcNode* next;//指向的下一条边 
        }ArcNode;

        typedef struct vnode {
            char data;
            ArcNode* firstarc = NULL;
        }vnode, adjlist[MAX_NUM];

        typedef struct {
            adjlist vex;
            int vexnum, arcnum;
        }Graph;

        //用邻接表实现DFS 
        void DFSTraverse(Graph g, int v) {
            visited[v] = true;
            cout << g.vex[v].data;
            int j = g.vex[v].firstarc->adjvex;
            ArcNode* p = g.vex[v].firstarc;
            while (p) {
                if (visited[p->adjvex]!=true) {
                    DFSTraverse(g, p->adjvex);
                }
                p = p->next;
            }
        }

        void initGraph(Graph& g) {
            int nvex, narc;//输入指向的顶点与所原先所依赖的顶点 
            ArcNode* s,*p;
            cout << "输入顶点数和边数";
            cin >> g.vexnum >> g.arcnum;
            cout << "输入各个顶点的数据";
            for (int i = 0; i < g.vexnum; i++) {
                cin >> g.vex[i].data;
            }
            cout << "输入边的指向顶点";
            //前插法建表 建立无向图 
            for (int i = 0; i < g.arcnum; i++) {
                s = (ArcNode*)malloc(sizeof(ArcNode));
                cin >> nvex >> narc;
                s->adjvex = nvex;
                s->next = g.vex[narc].firstarc;
                g.vex[narc].firstarc = s;
                p = (ArcNode*)malloc(sizeof(ArcNode));
                p->adjvex = narc;
                p->next = g.vex[nvex].firstarc;
                g.vex[nvex].firstarc = p;
            }

        }

        int main() {
            Graph g;
            initGraph(g);
            for (int i = 0; i < g.vexnum; i++) {
                visited[i] = false;
            }
            DFSTraverse(g, 0);
        }

> 用邻接矩阵表示图 遍历图的时间复杂度为O(n^2)
> 用邻接表表示图 遍历图的时间复杂度为O(n+e)
> **^_^**