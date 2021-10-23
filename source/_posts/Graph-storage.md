---
title: Graph_storage
date: 2021-10-23 14:45:12
tags: 数据结构
---

**图的存储结构**

- **邻接矩阵（图的数组表示法）**
        typedef struct ArcCell {//对于边的定义
            VRType adj;//定义顶点的关系类型  
            //对于无权图用0 1表示是否相邻
            //对于带权图，则为权值类型
            InfoType *info;//该边相关信息的指针
        } ArcCell, AdjMatrix[MAX_NUM][MAX_NUM];

- **用邻接矩阵实现图的定义：**
        typedef struct {
            VertexType vexs[MAX_NUM];//顶点信息
            AdjMatrix arcs;//边的信息
            int vexnum,arcnum;//图的顶点数、边数
            GraphKind kind;//图的种类标志
        } MGraph;

>邻接矩阵的特点：
>- 空间复杂度O(n^2)
>- 边的删除与插入容易 顶点的删除与插入不容易

------

- **用邻接表实现对于图的存储**

邻接表分为两部分：边链表、顶点表

- 边表的存储结构：
        typedef struct ArcNode {
            int adjvex;//表示该边所指向的顶点的位置
            VRType adj;//边的权值(带权图)
            struct ArcNode *nextarc;//指向下一个边的指针
            InfoType *info;//该边相关信息的指针
        } ArcNode;

- 顶点表的存储结构：
        typedef struct vnode {
            vertextype data;//用于存储顶点信息
            ArcNode *firstarc;//指向依附该顶点的边
        } vnode, adjlist[MAX_NUM];

- 用邻接表实现的图的存储结构：
        typedef struct {
            adjlist vertices;//顶点
            int vexnum, arcnum;//顶点数与边数
            int kind;图的类型
        } ALGraph;

>- 对于顶点多边少的图采用邻接图节省存储空间，空间复杂度O(n+e)
>容易找到任一顶点的第一个邻接点

- **有向图分邻接表与逆邻接表**
