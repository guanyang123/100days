100days
===========
day25 执行决策树
___________
```python
# 第一步 预处理
# 导入库
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.colors import ListedColormap
from sklearn.metrics import confusion_matrix
from sklearn.tree import DecisionTreeClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split

# 导入数据
dataset = pd.read_csv('Social_Network_Ads.csv')
X = dataset.iloc[:, 2:4].values
# print("X为："+str(X))
# print(X)
y = dataset.iloc[:, 4].values
#print("Y: \n"+str(Y))

# 拆分数据集
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.25, random_state=0)

# 特征量化 ，标准化数据
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test)

# 第二步 对测试集进行决策树分类拟合，分裂节点时的评价指标是信息增益
# 对于ID3这个算法，random_state这个参数可以不写
classifier = DecisionTreeClassifier(criterion='entropy', random_state=0)
classifier.fit(X_train, y_train)
#print(classifier.score(X_train ,y_train))

# 第三步 预测
y_pred = classifier.predict(X_test)
# print(y_pred)
# print(classifier.score(X_test,y_pred))

# 评估预测结果
cm = confusion_matrix(y_test, y_pred)
# print(cm)

# 第四步 绘制结果
X_set, y_set = X_train, y_train
X1, X2 = np.meshgrid(np.arange(start=X_set[:, 0].min() -
                               1, stop=X_set[:, 0].max() +
                               1, step=0.01), np.arange(start=X_set[:, 1].min() -
                                                        1, stop=X_set[:, 1].max() +
                                                        1, step=0.01))
plt.contourf(X1, X2, classifier.predict(np.array([X1.ravel(), X2.ravel()]).T).reshape(
    X1.shape), alpha=0.75, cmap=ListedColormap(('red', 'green')))
plt.xlim(X1.min(), X1.max())
plt.ylim(X2.min(), X2.max())
for i, j in enumerate(np.unique(y_set)):
    #==表判断，相同为Ture,不同为False，第二个0表示返回第0列
    plt.scatter(X_set[y_set == j, 0], X_set[y_set == j, 1],
                c=ListedColormap(('red', 'green'))(i), label=j)
plt.title('Decision Tree Classification(Training set)')
plt.xlabel('Age')
plt.ylabel('Estimated Salary')
# plt.legend（）函数主要的作用就是给图加上图例，即右上角小方框里的东西
plt.legend()
plt.show()

X_set, y_set = X_test, y_test
X1, X2 = np.meshgrid(np.arange(start=X_set[:, 0].min() -
                               1, stop=X_test[:, 0].max() +
                               1, step=0.01), np.arange(start=X_set[:, 1].min() -
                                                        1, stop=X_set[:, 1].max() +
                                                        1, step=0.01))
plt.contourf(X1, X2, classifier.predict(np.array([X1.ravel(), X2.ravel()]).T).reshape(
    X1.shape), alpha=0.75, cmap=ListedColormap(('red', 'green')))
plt.xlim(X1.min(), X1.max())
plt.ylim(X2.min(), X2.max())
for i, j in enumerate(np.unique(y_set)):
    plt.scatter(X_set[y_set == j, 0], X_set[y_set == j, 1],
                c=ListedColormap(('red', 'green'))(i), label=j)
plt.title('Decision Tree Classification(Test set)')
plt.xlabel('Age')
plt.ylabel('Estimated Salary')
plt.legend()
plt.show()


```

figure 1
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/25.2.png)  
figure 2
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/25.3.png)









