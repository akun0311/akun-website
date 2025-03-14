
# 最小生成树MST就是树的权值最小
# 最小生成树是为了什么
1. 最小生成树是想要在图里面得到一棵树, 为什么需要在图里面得到一棵树？
2. 代码实现部分建议去写一写。
3. Prim算法和Kruskal算法都是**贪心算法**。
4. 最小生成树一般是针对无向图的。
# Prim算法——加点法，一个点一个点加入
1. 任选一个节点当作当前节点的最小生成树，找到离当前最小生成树最近的节点，把它加入到树里面，以这样的方式不断地拓展这棵树，直到涵盖所有的节点为止。
2. Prim算法构造的最小生成树不是唯一的
3. Prim算法和边多边少是没有关系的，更适合稠密图。
# Kruskal算法——加边法，一条边一条边连接
1. Kruskal构造的最小生成树要连接所有的节点，并且让边的权重之和最小。
2. Kruskal算法是以找边为核心的，

| Prim算法    | 加点法 | 贪心算法 |
| --------- | --- | ---- |
| Kruskal算法 | 加边法 | 贪心算法 |




# 参考资料
1. https://www.bilibili.com/video/BV1o94y1E7hi/?spm_id_from=333.337.search-card.all.click&vd_source=86c038e54178b2c8db06f72a2c1b15da
2. https://www.bilibili.com/video/BV1wG411z79G/?spm_id_from=333.337.search-card.all.click&vd_source=86c038e54178b2c8db06f72a2c1b15da