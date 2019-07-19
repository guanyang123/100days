100days
===========
day44 K-均值聚类代码
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
# 导入K-均值聚类函数
from sklearn.cluster import KMeans

table = []
# range()只是打印1到6，7打印不到
for i in range(1, 7):
    # 抓取这个网页里的第1个表格
    table.append(pd.read_html('http://nba.hupu.com/stats/players/pts/%d' % i)[0])

# 所有数据纵向合并为数据框
players = pd.concat(table)
# 删除行标签为0的记录，因为换完页，行标签为0时，没有数据。
players.drop(0, inplace=True)
# 自变量为罚球命中率，因变量为命中率
# 取第一行到最后一行的，第九列的数据(0,1,..9)
X = players.iloc[1:, 9].values
Y = players.iloc[1:, 5].values
#print(X)

# 将带百分号的字符型转化为float型
x = []
for i in X:
    # 去掉百分号
    x.append(float(i.strip('%')))
x = np.array(x)/100
#print(x)

y = []
for j in Y:
    # 去掉百分号
    y.append(float(j.strip('%')))
y = np.array(y)/100
#print(y)

# 合并成矩阵
n = np.array([x.ravel(), y.ravel()]).T
#print(n)

# 绘制原始散点图
# 设置绘图风格，样式美化
plt.style.use('ggplot')
# 画散点图
plt.scatter(n[:, 0], n[:, 1])
plt.xlabel('free throw hit rate')
plt.ylabel('hit rate')
plt.show()

# 选择最佳的k值
X = n[:]
# 确定K值范围
K = range(1, int(np.sqrt(n.shape[0])))
GSSE = []
for k in K:
    SSE = []
    # 构造聚类器
    kmeans = KMeans(n_clusters=k, random_state=10)
    kmeans.fit(X)   # 聚类
    labels = kmeans.labels_      # 获取聚类标签
    centers = kmeans.cluster_centers_     # 获取每个簇的形心
    # set创建不重复集合
    for label in set(labels):
        # 不同簇内的数据减去该簇内的形心
        SSE.append(np.sum((np.array(n[labels == label,])-np.array(centers[label, :]))**2))
    # 总的误差
    GSSE.append(np.sum(SSE))

# 绘制K的个数与GSSE的关系
plt.plot(K, GSSE, 'b*-')
plt.xlabel('K')
plt.ylabel('Error')
plt.title('optimal solution')
plt.show()

# 调用sklearn的库函数
num_clusters = 6
kmeans = KMeans(n_clusters=num_clusters,random_state=1)
kmeans.fit(X)

# 聚类中心
centers = kmeans.cluster_centers_

# 绘制簇散点图
plt.scatter(x=X[:, 0], y=X[:, 1], c=kmeans.labels_)
# 绘制形心散点图
plt.scatter(centers[:, 0], centers[:, 1], c='k', marker='*')
plt.xlabel('free throw hit rate')
plt.ylabel('hit rate')
plt.show()
```
figure 1
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/44.1.PNG)  
figure 2
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/44.2.PNG)
figure 3
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/44.3.PNG)
  


