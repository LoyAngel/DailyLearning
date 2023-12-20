# Machine Learning

## 机器学习的基本概念
### 机器学习的常见术语
- 特征(属性)：特征是指用来描述数据的不同维度的特征，比如身高、体重、年龄等。
- 目标变量(标签)：目标变量是指我们要预测的变量，比如房价、销量等。
- 样本：样本是指数据集中的每一条数据，比如一条房屋信息、一条销售记录等。
- 知识表示：知识表示是指机器学习模型的输出结果，比如房价预测结果、销量预测结果等。
- 分类：机器学习的主要任务之一，指的是将数据分成不同的类别，比如将房屋分为不同的等级、将销量分为不同的等级等。
- 回归：机器学习的主要任务之一，指的是预测目标变量的值，比如预测房价、预测销量等。
### 机器学习的分类
- 监督学习：监督学习是指训练数据集中包含目标变量的数据集，比如房屋信息中包含房价信息，销售记录中包含销量信息等。
- 无监督学习：无监督学习是指训练数据集中不包含目标变量的数据集，比如房屋信息中不包含房价信息，销售记录中不包含销量信息等。无监督学习又分为聚类和密度估计。聚类指的是将数据分成不同的类别；密度估计指的是估计数据的概率密度函数。
### 机器学习应用开发步骤
1. 收集数据：包括爬取数据、从数据库中提取数据、公开源数据等。
2. 准备输入数据：包括数据清洗、数据转换、数据集成、数据规约等。
3. 分析输入数据： 包括数据可视化、特征选择等。
4. 训练算法： 包括数据集划分、特征工程、模型训练等。
5. 测试算法： 包括模型评估、模型预测等。

## kNN (k-Nearest Neighbor)，k近邻算法
参考网址：[kNN算法原理](https://www.cnblogs.com/ybjourney/p/4702562.html)
### 基本概念
#### kNN算法的基本思想
如果一个样本在特征空间中的k个最相似(即特征空间中最邻近)的样本中的大多数属于某一个类别，则该样本也属于这个类别，并具有这个类别上样本的特性。
#### kNN算法的Python实现
```python
import operator
import numpy as np

def createDataSet():
    group = np.array([[1.0,1.1],[1.0,1.0],[0,0],[0,0.1]])
    label = ['A','A','B','B']
    return group,label

def classify0(inX, dataSet, labels, k):
    """
    分类函数，使用了欧式距离公式，通过计算输入向量与训练样本的距离，选取距离最小的k个点，统计这k个点的类别，返回出现次数最多的类别
    :param inX: 输入向量
    :param dataSet: 训练样本集
    :param labels: 训练样本标签
    :param k: 选取距离最小的k个点
    """
    dataSetSize = dataSet.shape[0] # shape[0]返回矩阵的行数
    diffMat = np.tile(inX, (dataSetSize, 1)) - dataSet # tile函数将输入向量扩展为与训练样本相同大小的矩阵，然后计算差值
    sqDiffMat = diffMat ** 2
    sqDistances = sqDiffMat.sum(axis=1)
    distances = sqDistances ** 0.5
    print(f"距离：{distances}")
    sortedDistIndicies = distances.argsort()
    print(f"排序：{sortedDistIndicies}")
    classCount = {}

    # 选取距离最小的k个点，统计这k个点的类别
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]] # 按照距离从小到大的顺序访问标签
        print(f"第{i}个点的标签：{voteIlabel}")
        classCount[voteIlabel] = classCount.get(voteIlabel, 0) + 1 # 计算标签出现的次数
    print(f"未排序：{classCount}")
    sortedClassCount = sorted(classCount.items(), key=operator.itemgetter(1), reverse=True)
    print(f"排序后：{sortedClassCount}")
    return sortedClassCount[0][0]

group,labels = createDataSet()
classify0([0,0],group,labels,3)
```
### knn算法优缺点和适用场景
- 优点： 
    1. 简单，易于理解，易于实现，无需估计参数，无需训练；
    2. 适合对稀有事件进行分类；
    3. 特别适合于多分类问题(multi-modal,对象具有多个类别标签)；
    4. 对数据没有假设，准确度高，对异常值不敏感。
- 缺点：
    1. 计算复杂度高，空间复杂度高；
    2. 样本不平衡问题（即有些类别的样本数量很多，而其他样本的数量很少）；
    3. 一般数值型数据需要归一化；
    4. 可解释性差，无法给出数据的内在含义；
    5. 维数灾难（即随着维度的增加，“看似相近”的两个点之间的距离越来越大）；
    6. 由于kNN需要对每个测试样本计算与所有训练样本的距离，因此当训练集很大时，计算非常耗时。 
- 适用场景： 
    1. 多分类问题，比如手写数字识别；
    2. 预测与样本的距离相关性较高的情况，比如预测用户对某部电影的喜好程度；

## 决策树(Decision Tree)
参考网址：[决策树算法原理](https://www.cnblogs.com/ybjourney/p/4702562.html)
### 基本概念
#### 决策树的基本思想
决策树是一种基本的分类与回归方法，它代表的是对象属性与对象值之间的一种映射关系。树中每个节点表示某个对象，而每个分叉路径则代表的某个可能的属性值，而每个叶节点则对应从根节点到该叶节点所经历的路径所表示的对象的值。决策树学习的目的是为了产生一棵泛化能力强，即处理未见示例能力强的决策树。


## SVM (Support Vector Machine)， 支持向量机
参考网址：[零基础学SVM](https://zhuanlan.zhihu.com/p/24638007)  

![基本概念](https://pic2.zhimg.com/80/v2-d2b03cf98869849d1d6a4d91a05d6571_1440w.webp "基本概念")
### 基本概念

#### 决策面
决策面指的是将数据分成两类的分界线。
#### 分类间隔
分类间隔指的是决策面到最近的数据点的距离。
#### 支持向量
支持向量指的是离决策面最近的数据点。
#### 超平面
超平面指的是将数据分成两类的分界面。
#### SVM
SVM本质是一个二分类模型，它的基本模型定义为特征空间上的间隔最大的线性分类器，即支持向量机。


### 线性SVM的数学建模
#### 决策面方程
$$
w^Tx+b=0
$$
#### 分类间隔的计算模型
$$
d=\frac{|w^Tx+b|}{||w||}
$$
#### 约束条件
三个约束条件：
1. 如何判断是否存在一条直线能将样本点正确分类？
2. 如何判断决策面位于间隔区域的中轴线上？
3. 对于给定的决策面，如何找到对应的支持向量？  

分类讨论：  
将样本点分为两类，比如红和蓝，每个样本点xi加上一个类别标签$y_i$，$y_i∈{−1,1}$, 那么$y_i$可以表示为：
$$
y_i=
\begin{cases}
&+1 ,\text{ if $x_i$ is red} \\
&-1 ,\text{ if $x_i$ is blue}
\end{cases}
$$
则SVM优化的基本描述：
$$
\begin{cases}
&w^Tx_i+b≥+1 ,\text{ for $y_i=+1$} \\
&w^Tx_i+b≤-1 ,\text{ for $y_i=-1$}
\end{cases}
$$
#### SVM最优化问题基本描述
文字描述：找到一个决策面，使得所有样本点到决策面的距离最大。  
数学描述：
$$
\begin{cases}
&\min\limits_{w,b} \frac{1}{2}||w||^2 \\
&s.t. y_i(w^Tx_i+b)≥1 ,\text{ for $i=1,2,...,N$}
\end{cases}
$$

### 有约束最优化的数学模型
#### 有约束优化问题的几何意象
等式约束：$g(x)=0$ 的几何意义是 $d$ 维空间中 $d-1$ 维的曲面。  
不等式约束：$g(x)≥0$ 的几何意义是 $d$ 维空间中的 $d$ 维空间的子集。
#### 拉格朗日乘子法
##### 最优解特点分析
$f(w)=||w||^2$   

三大推论：
1. 原始目标函数$f(x)$的梯度向量$\nabla f(x)$与约束函数$g(x)=0$ 的切线方向垂直。
2. $f(x)$ 的梯度方向也必然与函数自身的等值线垂直。
3. 函数$f(x)$ 与约束函数$g(x)=0$ 的等值线在最优解点处相切，即两者在最优解点处的梯度方向相同或相反。  
##### 拉格朗日函数
$$
L(w,λ)=f(w)+λg(x) \\
g(x)=y_i(w^Tx_i+b)−1 = 0
$$
##### 不等式约束的拉格朗日函数
$$
L(w,λ_i)=f(x)+\sum\limits_{i=1}^n λ_ig_i(x) \\
g(x,p_i)=y_i(w^Tx_i+b)-1-p_i^2
$$
得到拉格朗日函数：
$$
L(w,λ_i,p_i)=f(x)+\sum\limits_{i=1}^n λ_i(y_i(w^Tx_i+b)-1-p_i^2)
$$
##### 最终结果
1. 求导化简结果
$$
\begin{cases}
&\frac{\partial L}{\partial w}=0 &\Rightarrow w=\sum\limits_{i=1}^n λ_iy_ix_i & (1) \\
&\frac{\partial L}{\partial b}=0 &\Rightarrow \sum\limits_{i=1}^n λ_iy_i=0 & (2)\\
&\frac{\partial L}{\partial λ_i}=0 &\Rightarrow y_i(w^Tx_i+b)-1-p_i^2=0 & (3)\\
&\frac{\partial L}{\partial p_i}=0 &\Rightarrow λ_ip_i^2=0 &(4)
\end{cases} \\
$$
由约束条件与(3)和(4)推断两种情况：
$$
\begin{cases}
&λ_i=0, &y_i(w^Tx_i+b)-1=g_i(x)<0 \\
&λ_i≠0, &y_i(w^Tx_i+b)-1=g_i(x)=0
\end{cases}
$$
#### KKT条件
KKT条件是指拉格朗日函数的最优性条件，它是最优化问题的充分条件，但不是必要条件。
即对于
$$
\begin{cases}
&\min\limits_{x} &f(x) \\
&s.t. &g(x)≤0
\end{cases}
$$
两种情况
1. 最优解在约束条件边界  
此时g(x)=0，由拉格朗日函数的最优性条件可知，f(x)的梯度方向与约束函数g(x)=0的切线方向相反，因此λ>0。
1. 最优解在约束条件内部  
此时g(x)<0，约束条件g(x)=0不起作用，因此λ=0。

因此KKT条件为：
$$
\begin{cases}
&g(x^*)≤0 \\
&λ≥0 \\
&λ^*g(x^*)=0
\end{cases}
$$
#### 拉格朗日对偶
拉格朗日对偶是指将一个原始最优化问题转化为与之等价的对偶形式，可以将有约束最优化问题转化为无约束最优化问题。
##### 原始目标函数(有约束)
$$
\begin{cases}
&\min\limits_{x} &f(x) \\
&s.t. &g_i(x)≤0 ,\text{ for $i=1,2,...,n$} \\
&&h_i(x)=0 ,\text{ for $i=1,2,...,l$}
\end{cases}
$$
##### 新构造的目标函数(无约束)
新构建目标函数:
$$
\theta_P(x)=\max\limits_{λ,μ:λ≥0} L(x,λ,μ)
$$

广义拉格朗日函数：
$$
L(x,λ,μ)=f(x)+\sum\limits_{i=1}^n λ_ig_i(x)+\sum\limits_{i=1}^l μ_ih_i(x)
$$

##### 对偶问题
$$
\begin{cases}
&\max\limits_{λ,μ:λ≥0} &\theta_P(x) \\
&s.t. &λ≥0
\end{cases}


