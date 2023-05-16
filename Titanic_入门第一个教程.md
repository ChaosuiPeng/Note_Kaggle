## 处理数据
### Library准备
两个常用的library
```python
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
```

Kaggle自带的notebook里面会载入当前competition用到的data，这里用os根据定义的路径列出所有文件名
```python
#list all files under the input directory
import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
```
![1684210960167](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/df401865-de76-44c1-af11-69822025898c)

### 载入数据集
```python
# load the training / test data (csv file)
train_data = pd.read_csv("/kaggle/input/titanic/train.csv")
test_data = pd.read_csv("/kaggle/input/titanic/test.csv")
```

如果想要瞅一眼载入了什么东西：

数据太多了，我们可以截个头五条看看。

⚠ 我们发现！！！有很多NaN。脑子：be careful when you deal with the data
```python
# show the first 5 rows
train_data.head() 
```
![1684211035420](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/3395bf36-e619-4ddb-abf3-7a2d4c9dfba9)

### filter
也可以根据features的值过滤，只看其中的一些行
```python
# pick certain rows, give me all the row where sex is female
train_data.loc[train_data.Sex == 'female']
```
![1684211226049](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/99a86478-f6ff-4655-b656-12583cc72df8)

甚至，可以只要 某些特定行 的 某一列数据（两种方式）
```python
train_data.loc[train_data.Sex == 'female'].Survived
```
```python
# filter
women = train_data.loc[train_data.Sex == 'female']["Survived"]
women
```
![1684211317088](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/8e381cef-435e-47ae-947d-75f78a4cd402)

对截取后的数据，可以打竖统计sum或者数数有多少行
```python
sum(women)  # 上面的survived用0和1表示，这个操作目的是统计多少人1
```
```python
len(women)  # 一行一个人，其实这里是统计人数
```

## Random Forest Model
载入第三个常用的库sklearn，准备好我们训练的”正确答案“、认为重要的训练特征们
```python
from sklearn.ensemble import RandomForestClassifier

y = train_data["Survived"]
features = ["Pclass", "Sex", "SibSp", "Parch"]
```

至于train_data，我们只需要某些列（train_data在上面从csv读进来了），瞅一眼
```python
train_data[features]
```
![1684211830737](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/2ef6b677-8ee1-4933-9515-7a9e938cee46)

⚠ 我们又发现！这里的Sex是字符串。脑子：不能直接用，要变成0和1
介绍一个get_dummies函数
```python
# string in our data need to be further processed: transfer to 0 and 1
X = pd.get_dummies(train_data[features])
X_test = pd.get_dummies(test_data[features])
```

现在我们可以把训练数据丢进（库自带的）模型中
```python
model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=1)
model.fit(X, y)
```

fit完之后，我们丢测试数据，看看预测的结果
```python
predictions = model.predict(X_test)
predictions # an array of binary values of 0 and 1
```
![1684212195624](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/2b7ade8b-0831-45d0-beb9-7a3f90875d75)

按照这个Competition要求的输出格式，拼一个dataframe。

惯例再看看长什么样（检查！）
```python
# keep the order of the id the same as predictions
output = pd.DataFrame({'PassengerId': test_data.PassengerId, 'Survived': predictions})
output.head()
```
![1684212279703](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/af189313-2d66-4206-8d1f-4b805afcf0f7)

输出
```python
output.to_csv('submission.csv', index=False)
```
