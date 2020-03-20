## Thinking1：排序模型按照样本生成方法和损失函数的不同，可以划分成Pointwise, Pairwise, Listwise三类方法，这三类排序方法有何区别
- Pointwise,针对单一文档；Pairwise，关注文档的顺序关系；Listwise，将以此Query对应的所有搜索结果列表作为一个训练样例
- Pairwise 与 Listwise 考虑到了文档的相关性，及多样性
## Thinking2：排序模型按照结构划分，可以分为线性排序模型、树模型、深度学习模型，这些模型都有哪些典型的代表？
- RankNet 基于神经网络的排序算法 \ LambdaRank \ LambdaMART
## Thinking3：NDCG如何计算
- DCG/IDCG DCG：折损累计增益； IDCG：理想情况下最大的DCG值
## Thinking4：搜索排序和推荐系统的相同和不同之处有哪些
- 推荐系统着重多样性、是否发散的、无意识的主动推荐 ，搜索排序更关注准确性，有意识的被动推荐
## Thinking5：Listwise排序模型能否应用到推荐系统中
- 推荐系统一般不考虑 顺序问题，一般是员工porntwise