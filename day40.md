100days
===========
day40 深度学习基础Python，TensorFlow和Keras
```python
import numpy as np
import matplotlib.pyplot as plt
import os
import cv2
import random
import pickle
from tqdm import tqdm

# 数据集的路径
DATADIR = "C:/Users/86178/Desktop/PetImages"
CATEGORIES = ["DOG", "CAT"]
# for循环用于遍历CATEGORIES,把取出来的图片存储在变量category
for category in CATEGORIES:
    # 创建路径
    path = os.path.join(DATADIR, category)
    # 迭代遍历每个图片，在Python中可以使用os.listdir()函数获得指定目录中的内容。
    for img in os.listdir(path):
        # 用来读取图片文件中的数据
        img_array = cv2.imread(os.path.join(path, img), cv2.IMREAD_GRAYSCALE)
        # 转换成图像展示
        plt.imshow(img_array,cmap='gray')
        #plt.show()
        break
    break
#print(img_array)
# 看下array的形状
#print(img_array.shape)

IMG_SIZE = 50
#resize图像缩放函数
new_array = cv2.resize(img_array, (IMG_SIZE, IMG_SIZE))
plt.imshow(new_array, cmap='gray')
#plt.show()
# size设置成50有些模糊，尝试下100
IMG_SIZE = 100
new_array = cv2.resize(img_array,(IMG_SIZE,IMG_SIZE))
plt.imshow(new_array, cmap='gray')
#plt.show()

training_data = []
def create_training_data():
    for category in CATEGORIES:
        path = os.path.join(DATADIR,category)
        # 得到分类，0=dog,1=cat
        class_num = CATEGORIES.index(category)
        for img in tqdm(os.listdir(path)):
            try:
                img_array = cv2.imread(os.path.join(path,img),cv2.IMREAD_GRAYSCALE)
                new_array = cv2.resize(img_array,(IMG_SIZE,IMG_SIZE))
                # 加入训练集数据中
                training_data.append([new_array,class_num])
            # 为了保证输出是整洁的
            except Exception as e:
                pass
create_training_data()
# len() 方法返回对象（字符、列表、元组等）长度或项目个数。
#print(len(training_data))
# shuffle()函数是将training_data里的数据随机打乱
random.shuffle(training_data)
# 遍历training_data里的第0列到第9列
for sample in training_data[:10]:
    print(sample[1])

X = []
y = []
for features, label in training_data:
    # 在X里面追加上features
    X.append(features)
    y.append(label)
    # reshape函数用处：将一个矩阵重新生成任意维度的矩阵（元素个数内）
    # 行数
print(X[0].reshape(-1, IMG_SIZE,IMG_SIZE, 1))
X = np.array(X).reshape(-1, IMG_SIZE, IMG_SIZE, 1)

# 以二进制的方式写入打开的文件中
pickle_out = open("../datasets/X.pickle","wb")
pickle.dump(X, pickle_out)
pickle_out.close()

pickle_out = open("../datasets/y.pickle","wb")
pickle.dump(y,pickle_out)
pickle_out.close()

# 我们总是可以将它加载到当前脚本中，或者通过doing加载一个全新的脚本
pickle_in = open("../datasets/X.pickle","rb")
# pickle.load()方法，是反序列化对象，将pickle_in中的数据解析为一个python对象
X = pickle.load(pickle_in)
pickle_in = open("../datasets/y.pickle","rb")
y = pickle.load(pickle_in)


```

figure 1
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/40.1.PNG)  
figure 2
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/40.2.PNG)
figure 3
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/40.3.PNG)
