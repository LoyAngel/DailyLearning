# SVM (Support Vector Machine)
参考网址：[零基础学SVM](https://zhuanlan.zhihu.com/p/24638007)  

![基本概念](https://pic2.zhimg.com/80/v2-d2b03cf98869849d1d6a4d91a05d6571_1440w.webp "基本概念")
## 基本概念

### 决策面
决策面指的是将数据分成两类的分界线。
### 分类间隔
分类间隔指的是决策面到最近的数据点的距离。
### 支持向量
支持向量指的是离决策面最近的数据点。
### 超平面
超平面指的是将数据分成两类的分界面。
### SVM
SVM本质是一个二分类模型，它的基本模型定义为特征空间上的间隔最大的线性分类器，即支持向量机。


## 线性SVM的数学建模
### 决策面方程
$$
w^Tx+b=0
$$
### 分类间隔的计算模型
$$
d=\frac{|w^Tx+b|}{||w||}
$$
### 约束条件
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
### SVM最优化问题基本描述
文字描述：找到一个决策面，使得所有样本点到决策面的距离最大。  
数学描述：
$$
\begin{cases}
&\min\limits_{w,b} \frac{1}{2}||w||^2 \\
&s.t. y_i(w^Tx_i+b)≥1 ,\text{ for $i=1,2,...,N$}
\end{cases}
$$

## 有约束最优化的数学模型
### 有约束优化问题的几何意象
等式约束：$g(x)=0$ 的几何意义是 $d$ 维空间中 $d-1$ 维的曲面。  
不等式约束：$g(x)≥0$ 的几何意义是 $d$ 维空间中的 $d$ 维空间的子集。
### 拉格朗日乘子法
#### 最优解特点分析
$f(w)=||w||^2$   

三大推论：
1. 原始目标函数$f(x)$的梯度向量$\nabla f(x)$与约束函数$g(x)=0$ 的切线方向垂直。
2. $f(x)$ 的梯度方向也必然与函数自身的等值线垂直。
3. 函数$f(x)$ 与约束函数$g(x)=0$ 的等值线在最优解点处相切，即两者在最优解点处的梯度方向相同或相反。  
#### 拉格朗日函数
$$
L(w,λ)=f(w)+λg(x) \\
g(x)=y_i(w^Tx_i+b)−1 = 0
$$
#### 不等式约束的拉格朗日函数
$$
L(w,λ_i)=f(x)+\sum\limits_{i=1}^n λ_ig_i(x) \\
g(x,p_i)=y_i(w^Tx_i+b)-1-p_i^2
$$
得到拉格朗日函数：
$$
L(w,λ_i,p_i)=f(x)+\sum\limits_{i=1}^n λ_i(y_i(w^Tx_i+b)-1-p_i^2)
$$
#### 最终结果
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
&λ_i=0, &y_i(w^Tx_i+b)-1>0 \\
&λ_i≠0, &y_i(w^Tx_i+b)-1=0
\end{cases}
$$
### KKT条件
KKT条件是指拉格朗日函数的最优性条件，它是最优化问题的充分条件，但不是必要条件。
两种情况
1. 最优解在约束条件边界
f(x)的梯度方向与约束函数g(x)=0的切线方向相反，因此λ>0。
1. 最优解在约束条件内部
在区域内，约束条件g(x)=0不起作用，因此λ=0。

因此KKT条件为：
$$
\begin{cases}
&g(x^*)≤0 \\
&λ≥0 \\
&λ^*g(x^*)=0
\end{cases}
$$
### 拉格朗日对偶
拉格朗日对偶是指将一个原始最优化问题转化为与之等价的对偶形式，可以将有约束最优化问题转化为无约束最优化问题。
#### 原始目标函数(有约束)
$$
\begin{cases}
&\min\limits_{x} &f(x) \\
&s.t. &g_i(x)≤0 ,\text{ for $i=1,2,...,n$} \\
&&h_i(x)=0 ,\text{ for $i=1,2,...,l$}
\end{cases}
$$
#### 新构造的目标函数(无约束)
新构建目标函数:
$$
\theta_P(x)=\max\limits_{λ,μ:λ≥0} L(x,λ,μ)
$$

广义拉格朗日函数：
$$
L(x,λ,μ)=f(x)+\sum\limits_{i=1}^n λ_ig_i(x)+\sum\limits_{i=1}^l μ_ih_i(x)
$$

#### 对偶问题
$$
\begin{cases}
&\max\limits_{λ,μ:λ≥0} &\theta_P(x) \\
&s.t. &λ≥0
\end{cases}


