2019/7/13  
随机森林
===========  
1、`随机森林`构建多个决策树，并将它们合并在一起，得到更准确、更稳定的预测。随机森林是用来分类和回归的监督集成学习模型。  

2、`集成学习模型`聚合了多个机器学习模型，从而提高了整体性能。这背后的逻辑是，使用的每一个模型在单独使用时都是弱的，但在集成中放在一起时则是强的。在随机森林的情况下，使用大量的决策树作为弱因子，并对它们的输出进行聚合，结果表示强集合。  

3、`随机森林算法`有两个步骤，一个是随机森林的生成，另一个是随机预测在第一步中创建森林分类器。  

4、`随机森林算法和决策树算法的不同之处`在于，在随机森林中，查找根节点和分割特征节点的过程将随机运行。在随机森林算法中的决策树，`每棵树的生长方式`如下：1.如果训练集中的病例数为N，有放回的随机抽取n个，这个样本将是生成决策树的训练集。2.（特征的随机选取）对于每个样本，如果有M个输入变量（或者特征），指定一个常数m，然后随机的从M个特征中选取m个特征子集，然后将m个特征中最优的分裂特征用来分裂节点。

5、`随机森林的预测`分为以下三步：1.使用每一个随即创建的决策树的规则来预测测试特征的结果（目标）。2.计算每个预测目标的票数。3.获得票数最高的预测目标视为随机森林算法的最终预测。  

6、`RandomForestClassifier()函数的用法`:`n_estimators` : integer, optional (default=10)随机森林中树的数量；`criterion` : string, optional (default=”gini”)树分裂的规则：gini系数，entropy熵；`max_features` : int, float, string or None, optional (default=”auto”)查找最佳分裂所需考虑的特征数，int：分裂的最大特征数，float：分裂的特征占比，auto、sqrt：sqrt(n_features)，log2：log2(n_features)，None：n_features;`max_depth `: integer or None, optional (default=None)树的最大深度；`min_samples_split`：int, float, optional (default=2)最小分裂样本数；`min_samples_leaf` : int, float, optional (default=1)最小叶子节点样本数；`min_weight_fraction_leaf` : float, optional (default=0.)最小叶子节点权重；`max_leaf_nodes` : int or None, optional (default=None)最大叶子节点数；`min_impurity_split` : float, optional (default=1e-7)分裂的最小不纯度；`bootstrap` : boolean, optional (default=True)是否使用bootstrap；oob_score : bool (default=False)是否使用袋外（out-of-bag）样本估计准确度；
`n_jobs` : integer, optional (default=1)并行job数，-1 代表全部；`random_state` : int, RandomState instance or None, optional (default=None)随机数种子；`verbose` : int, optional (default=0)Controls the verbosity of the tree building process.（控制树冗余？）;`warm_start` : bool, optional (default=False)如果设置为True，在之前的模型基础上预测并添加模型，否则，建立一个全新的森林；`class_weight` : dict, list of dicts, “balanced”,“balanced” 模式自动调整权重，每类的权重为 n_samples / (n_classes * np.bincount(y))，即类别数的倒数除以每类样本数的占比。


