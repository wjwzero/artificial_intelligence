## thinking1 在CTR点击率预估中，使用GBDT+LR的原理是什么
- 自动发现有效的特征及特征组合，弥补人工经验不足缩短LR实验周期
- 具有stacking思想的二分类器模型，用来解决二分类问题
- 通过GBDT将特征进行组合，然后传入给线性分类器
- LR对GBDT产生的输入数据进行分类（使用L1正则化防止过拟合）
    - GBDT 有多颗CART回归树组成，将累加所有树的结果作为最终结果
    - 采用梯度迭代 Gradient Boosting 通过贴袋多颗树来共同决策
    - 每一次简历模型是在之前模型损失函数的梯度下降方向
## thinking2 Wide&Deep的模型结构是怎样的，为什么能通过具备记忆和泛化能力(memorization and generalization)
- wide&Deep 是深度模型与线性模型的结合；
- memorization 记忆能力，学习items或者features之间的相关频率，在历史数据中探索相关性的可能性；
- generalization，泛化（推理）能力 ，基于相关性的传递，去探索一些过去没有出现过的特征组合

## thinking3 CTR预估中，使用FM与DNN结合的方式，有哪些结合的方式，代表模型有哪些？
- "串行"方式，代表模型有FNN (Factorisation-machine supported Neural Networks),在此模型中，稀疏特征先通过Dense Embedding进行编码，而Dense Embedding层的参数是由FM模型初始化的，计算得到的结果再进入DNN进行高阶特征的抽取和计算
- "并行"方式，代表模型有DeepFM,在此模型中，稀疏特征经过Dense Embedding层，一路进入FM层，用来计算二阶特征；另外一路进入DNN中计算高阶特征，其中FM层的一阶特征是由稀疏特征经过线性计算得到。最后FM层的输出结果与DNN的输出结果拼接起来一起进入DeepFM的输出层。

## Thinking4 Surprise工具汇中的baseline算法原理是怎样的？BaselineOnly和KNNBaseline有什么区别？
- Baseline算法原理是 鸡舍用户u对物品i的评价，是由物品的平均评价和无品i获得评价的偏差以及用户打分差纸盒计算得到

    $$b_{ui} = \mu + b_u + b_i $$
    - $b_u$和$b_i$可通过交替最小二乘ALS优化以下函数得到：
    $$\min_{b_*}\sum_{(u,i)\in K}(r_{ui} - \mu - b_u - b_i)^2 +\lambda_1(\sum_{u}b_u^2 + \sum_{i}b_i^2)$$
    
    - 此基础上KNNBaseline在计算$\hat{r}_{ui}$时考虑到了用户u的k个邻居用户对物品i的评价
    $$\hat{r}_{ui} = b_{ui} + \frac{\sum_{v\in{N_i}^k(u)}sim(u, v)\cdot(r_{vi} - b_{vi})}{\sum_{v\in{N_i}^k(u)}sim(u,v)}$$

## Thinking5 GBDT和随机森林都是基于树的算法，它们有什么区别？
- 均基于树模型，且属于集成算法
- GBDT采用Boosting方法，通过多个CART树提升训练结果的集成方法来提高预测精度。
- 随机森林采用的是Bagging方法，通过自采样的方法生成多并行式的分类器，通过“少数服从多数”的原则来确定最终的结果

## Thinking6 基于邻域的协同过滤多有哪些算法，请简述原理？
- UserCF 基于用户的系统协同过滤: 通过当前用户u与其相似用户v的相似度，以及相似用户v对兴趣物品i的兴趣程度，来推测当前用户对物品i的兴趣度。 按照用户u相似的k个用户的所有兴趣物品，依据用户u对其兴趣程度进行推荐。
- ItemCF 基于物品的协同过滤： 通过用户u对物品i的k邻物品的兴趣程度来计算用户u对物品i的兴趣程度根据用户u对候选物品列表汇总的候选物品兴趣程度给用户推荐。