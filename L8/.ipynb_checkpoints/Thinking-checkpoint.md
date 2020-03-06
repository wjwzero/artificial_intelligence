## thinking1 什么是近似最近邻查找，常用的方法有哪些
- 近似最近邻查找是以降低精度为代价处理大量数据的相似度过滤的一种方式；常用的方法有 MinHash + LSH、SimHash算法
    - minhash ：


## thinking2 为什么两个集合的minhash只相同的概率等于这两个集合的Jaccard相似度
- 对应元素有三种可能：
    - a：两元素均存在有效值且相同
    - b: 两元素其中一个元素存在有效值且不同
    - c: 两元素均不存在
c情况对结果没影响，所以忽略
P(h(Ci)=h(Cj))=P(删除a类后的，首次a)=a的个数/所有=a(a+b)

## thinking3 simhash在计算文档相似度的作用是怎样的？
- 主要用于获得fingerprint即文档特征指纹
- 通过Hamming 计算小相似度

## Thinking4：为什么YouTube采用期望观看时间作为评估指标

- CTR指标对于视频搜索具有一定的欺骗性，所以用观看时长作为指标

## Thinking5 为什么YouTube在排序阶段没有采用经典的LR（逻辑回归）当作输出层，而是采用了Weighted Logistic Regression？

- 增加了观看时长作为指标