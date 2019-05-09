100days
===========
day13 SVM
___________
```python
# 第一步 预处理
# 导入库
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# 导入数据
dataset = pd.read_csv('Social_Network_Ads.csv')
# 取所有行第2列和第3列的所有数据，可写成iloc[:,2:4].values
X = dataset.iloc[:, [2, 3]].values
# 取所有行第4列的内容
Y = dataset.iloc[:, 4].values
#print("dataset: \n"+str(dataset))
#print("X: \n"+str(X))
#print("Y: \n"+str(Y))

# 拆分数据集合为训练集合和测试集合
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y, test_size=0.25, random_state=0)
# print(X_train)

# 特征量化，标准化数据
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.fit_transform(X_test)
# print(X_train)
# print(X_test)

# 第二步 应用sklearn中的SVC
from sklearn.svm import SVC
classifier = SVC(kernel='linear', random_state=0)
classifier.fit(X_train, Y_train)

# 第三步 预测
Y_pred = classifier.predict(X_test)
# print(Y_pred)

# 评估预测结果
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(Y_test, Y_pred)
# print(cm)

# 第四步 绘制结果
from matplotlib.colors import ListedColormap
X_set, y_set = X_train, Y_train
print("y_set:" + str(y_set))
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
    #==表判断，相同为Ture,不同为False，第二个0表示返回第0列
    plt.scatter(X_set[y_set == j, 0], X_set[y_set == j, 1],
                c=ListedColormap(('red', 'green'))(i), label=j)
plt.title('SVM(Training set)')
plt.xlabel('Age')
plt.ylabel('Estimated Salary')
# plt.legend（）函数主要的作用就是给图加上图例，即右上角小方框里的东西
plt.legend()
# plt.show()

from matplotlib.colors import ListedColormap
X_set, y_set = X_test, Y_test
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
plt.title('SVM(Test set)')
plt.xlabel('Age')
plt.ylabel('Estimated Salary')
plt.legend()
# plt.show()





```
figure 1
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/13.21.PNG)  
figure 2
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/13.22.PNG)
