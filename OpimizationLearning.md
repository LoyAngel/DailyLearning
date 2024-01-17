# Opimization Learning 

## 前置知识
二次函数矩阵式：
$$
f(x)=\frac{1}{2}x^THx+b^Tx+c
$$
其一阶导数:
$$
\nabla f(x)=Hx+b
$$
其二阶导数,即Hessian矩阵:
$$
\nabla^2 f(x)=H
$$

## 线性搜索
### 进退法
本质是找到函数的一个单峰区间，方便后续搜索。  
步骤为：
1. 选取初始点$x_0, h_0$，计算$f(x_0)$,置 $k=0$；
2. 令$x_{k+1}=x_k+h_k$，计算$f(x_{k+1})$；若$f(x_{k+1})<f(x_k)$，转3；否则，转4；
3. 加大步长。即$h_{k+1}=2h_k,x=x_k,x_k=x_{k+1},f(x_k)=f(x_{k+1}),k=k+1$，转2；
4. 反向搜索或输出。若$k=0$，令$h_1=-h_0,x=x_1,x_1=x_0,f(x_1)=f(x_0),k=1$，转2；否则停止迭代。
5. 令$a=min\{x,x_{k+1}\}, b=max\{x,x_{k+1}\}$，输出$[a,b]$。
### 黄金分割法
理论依据：如果$f(x)$在区间$[a,b]$上是单峰的，且只有一个极小值，且区间$[a,b]$为搜索区间，那么对任意$x1,x2∈[a,b]$, 如果$f(x_1)<f(x_2)$，则搜索区间可以收缩为$[a,x_2]$，否则搜索区间可以收缩为$[x_1,b]$。  
步骤：
1. 确定初始搜索区间$[a,b]$和误差限$\epsilon$
2. 计算初始试探点$p_0=a_0+0.382(b_0-a_0)$, $q_0=a_0+0.618(b_0-a_0)$，计算$f(p_0),f(q_0)$，置$k=0$；若$f(p_0)<f(q_0)$，转3；否则，转4；
3. 计算左试探点，若$|q_k-a_k|<=\epsilon$，停止迭代，输出$[a_k,q_k]$；否则，令$a_{k+1}=a_k,b_{k+1}=q_k,f(q_{k+1})=f(q_k),q_{k+1}=q_k,p_{k+1}=a_{k+1}+0.382(b_{k+1}-a_{k+1})$，转2；
1. 计算右试探点，若$|b_k-p_k|<=\epsilon$，停止迭代，输出$[p_k,b_k]$；否则，令$a_{k+1}=p_k,b_{k+1}=b_k,f(p_{k+1})=f(p_k),p_{k+1}=q_k,q_{k+1}=a_{k+1}+0.618(b_{k+1}-a_{k+1})$，转2；


## Hessian矩阵 与 严格全局极小点(不考)
### 概念
Hessian矩阵是一个函数的二阶偏导数构成的方阵，它描述了函数的局部曲率。
严格全局极小点是指函数的极小点，且在该点的Hessian矩阵是正定矩阵。
### 计算
如何根据Hessian矩阵判断一个点是否是严格全局极小点？
首先，Hessian矩阵是一个对称矩阵，所以可以对其进行特征值分解，得到特征值$\lambda_1,\lambda_2,...,\lambda_n$，特征向量$v_1,v_2,...,v_n$。
然后，根据特征值的符号判断：
1. 当所有特征值都大于0时，Hessian矩阵是正定矩阵，该点是严格全局极小点。
2. 当所有特征值都小于0时，Hessian矩阵是负定矩阵，该点是严格全局极大点。
3. 当特征值有正有负时，Hessian矩阵是不定矩阵，该点不是极值点。
4. 当特征值有正有0时，Hessian矩阵是半正定矩阵，该点是极小点。
5. 当特征值有负有0时，Hessian矩阵是半负定矩阵，该点是极大点。

## 序列收敛(不考)
### 概念
对于$\lim\limits_{k\rightarrow\infty}x_k=x'$，如果存在正数$q$和$p$，使得$\lim\limits_{k\rightarrow\infty}\frac{\|x_{k+1}-x'\|}{\|x_k-x'\|^p}=q$，则称序列$\{x_k\}$是p阶收敛的，q是收敛速度。
1. 线性收敛：$0<q<1, p=1$
2. 超线性收敛：$q=0, p=1$
3. p阶收敛：$q=C, p>1$  

$x'$是序列的极限点。

## 最速梯度下降法
### 概念
最速梯度下降法是梯度下降法的一种改进方法。  
它的思想是：负方向梯度的方向是函数下降最快的方向，所以在每一步迭代中，沿着负梯度方向进行迭代，可以使得函数值下降最快。因此，取当前迭代点的负梯度方向作为搜索方向，进行一维搜索，找到最优步长，然后沿着该方向进行迭代，直到满足终止条件。
### 步骤
#### 最速梯度下降法计算步骤
1. 选取初始点$x_0$，给定终止误差$\epsilon$，置$k=0$；
2. 计算$f(x_k)$的梯度$g_k$，当$\|g_k\|<\epsilon$时，停止迭代，得到近似解$x^*=x_k$；否则，进行第3步；
3. 取$p_k=-g_k$；
4. 进行一维搜索，即求$a_k$，使得$f(x_k+a_kp_k)=\min\limits_{a\geq0}f(x_k+a p_k)$；一般来说，$a_k=\frac{g_k^Tg_k}{g_k^THg_k}$, 或者求导$\eta_k=\frac{\partial f(x_k+a p_k)}{\partial a}$，令$\eta_k=0$，求得最优步长$a_k$；
5. 令$x_{k+1}=x_k+a_kp_k$，置$k=k+1$，转第2步。
#### 最优步长计算步骤
微分法
因为要找寻$a$使得$f(x_k+a p_k)=\min\limits_{a\geq0}f(x_k+a p_k)$，所以可以对$f(x_k+a p_k)$求导，令导数为0，求得最优步长$a$。

### 代码实现
```python
import numpy as np
import math

# 所求函数
def f(x1, x2):
    return 3*x1**2 + 2*x2**2 - 4*x1 - 6*x2
# 梯度
def grad(x1, x2):
    return np.array([6*x1 - 4, 4*x2 - 6])
# 求模
def norm(x1, x2):
    return math.sqrt(x1**2 + x2**2)
# 求最优步长，这里直接用导数求导后相除得到（自己计算）
def get_lamda(x1, x2, p):
    return (4*p[0]+6*p[1]-6*x1*p[0]-4*x2*p[1]) / (6*p[0]**2 + 4*p[1]**2)
# 最速梯度下降法 
def steepest_descend_method(x1, x2, e):
    a = 0
    while True:
        g = grad(x1, x2)
        print(f'{i}Turn,x1={x1}, x2={x2}, f(x1, x2)={f(x1, x2)}, \n\tnorm = {norm(g[0], g[1])}, a = {a}, g = {g}')
        if norm(g[0], g[1]) < e:
            break
        else:
            p = -g
            a = get_a(x1, x2, p)
            x1 = x1 - a * grad(x1, x2)[0]
            x2 = x2 - a * grad(x1, x2)[1]
            x1 = round(x1, 3)
            x2 = round(x2, 3)

steepest_descend_method(10, 10, 0.1)
```

## 牛顿迭代法
### 概念
牛顿迭代法是一种求解方程的迭代方法，它是一种二阶收敛的方法。  
它的思想是: 用一阶泰勒展开式去逼近函数，然后求解逼近的方程，得到下一个迭代点，直到满足终止条件。  
一阶函数牛顿法公式 ： $x_{k+1}=x_k-\frac{f'(x_k)}{f''(x_k)}$  
多元函数牛顿法公式 ： $x_{k+1}=x_k-H_k^{-1}g_k$ , $H_k$是$f(x_k)$的Hessian矩阵，$g_k$是$f(x_k)$的梯度。  
阻尼牛顿法公式： $x_{k+1}=x_k-a_kH_k^{-1}g_k$ , $a_k$是步长，增加线性搜索，防止迭代点跑出函数定义域。  
高斯牛顿法公式： $x_{k+1}=x_k-(J_k^TJ_k)^{-1}J_k^Tf(x_k)$ , $J_k$是$f(x_k)$的雅克比矩阵。
### 阻尼牛顿法步骤
1. 选取初始点$x_0$，给定终止误差$\epsilon$，置$k=0$；
2. 计算$f(x_k)$的梯度$g_k$，当$\|g_k\|<\epsilon$时，停止迭代，得到近似解$x^*=x_k$；否则，进行第3步；
3. 计算$f(x_k)$的Hessian矩阵$H_k$，计算阻尼因子$a_k$，计算下一个迭代点$x_{k+1}=x_k-a_kH_k^{-1}g_k$，置$k=k+1$，转第2步。
4. 阻尼因子$a_k$的计算方法有很多种，这里介绍一种：$a_k=\min\{1,\frac{1}{2}\|\nabla f(x_k)\|_2\}$
5. 令$x_{k+1}=x_k-a_kH_k^{-1}g_k$，置$k=k+1$，转第2步。
### 代码实现
```python
import numpy as np
import matplotlib.pyplot as plt
ax=plt.axes(projection='3d')
def f(x):
    return x[0][0]**2+x[0][1]**2
def grad(x):
    '''函数梯度'''
    return 2*x
def H(x):
    '''Hession矩阵'''
    h=np.array([[2,0],
                [0,2]])
    return h
x=np.arange(-10,10,0.1)
y=np.arange(-10,10,0.1)
x,y=np.meshgrid(x,y)
z=x**2+y**2
x0=np.mat([10,9]).T
xt=[x0]
for i in range(10):
    x0=x0-np.dot(np.linalg.inv(H(x0)),grad(x0))
    xt.append(x0)
xt_x=[]
xt_y=[]
xt_z=[]
for i in xt:
    xt_x.append(i[0][0])
    xt_y.append(i[1][0])
    xt_z.append(i[0][0]**2+i[1][0]**2)
ax.plot_surface(x,y,z,cmap='rainbow')
ax.scatter(xt_x,xt_y,xt_z,color='red')
plt.show()
```

## 拟牛顿法
### 概念
拟牛顿法是一种求解方程的迭代方法，它是一种二阶收敛的方法。
它的思想是: 与牛顿法类似，用一阶泰勒展开式去逼近函数，然后求解逼近的方程，得到下一个迭代点，直到满足终止条件。但是它的Hessian矩阵不是精确的，而是用一种近似的方法去求解，这样可以减少计算量。  
#### SR1
公式：$H_{k+1}=H_k+\frac{(y_k-H_ks_k)(y_k-H_ks_k)^T}{(y_k-H_ks_k)^Ts_k}$  
思想：用$H_k$去近似$H_{k+1}$，使得$H_{k+1}$满足拟牛顿条件。

## 最小二乘法矩阵形式
### 概念
最小二乘法是一种数学优化技术，它通过最小化误差的平方和寻找数据的最佳函数匹配。  
它的思想是：  
当数据不满足线性关系时，可以通过最小二乘法拟合出一条直线，使得数据与直线的误差平方和最小。为了使误差平方和最小，需要对误差平方和求导，令导数为0，求得最优解。  
最小二乘法的矩阵形式的推导：  
1. 最小二乘法矩阵式是求$||Ax-b||^2$的最小值。
2. 令$||Ax-b||_2^2=(Ax-b)^T(Ax-b)= x^TA^TAx-b^TAx-x^TA^Tb+b^Tb$，对$x$求导，令导数为0，得到$A^TAx=A^Tb$。  
(PS: 矩阵求导：$f(x)=x^TAx$，则$\frac{\partial f(x)}{\partial x}=Ax+A^Tx$; A为对称矩阵，$Ax+A^Tx=2Ax$; $f(x)=b^Tx$，则$\frac{\partial f(x)}{\partial x}=b$)
3. 求解$A^TAx=A^Tb$，得到最优解$x=(A^TA)^{-1}A^Tb$。

## KT条件
推导见MLLearning.md KKT条件

KKT条件是指拉格朗日函数的最优性条件，它是最优化问题的充分条件，但不是必要条件。
即对于
$$
\begin{cases}
&\min\limits_{x} &f(x) \\
&s.t. &g_i(x)\geq0 ,\text{ for $i=1,2,...,n$} \\
&&h_i(x)=0 ,\text{ for $i=1,2,...,l$}
\end{cases}
$$
KKT条件为：
$$
\begin{cases}
\bigtriangledown f(x^*)-\sum\limits_{i=1}^n λ_i^*\bigtriangledown g_i(x^*)-\sum\limits_{i=1}^l μ_i^*\bigtriangledown h_i(x^*)=0 \\
h_i(x^*)=0 \\
g_i(x^*)\lambda_i^*=0 \\
λ_i^*≥0, g_i(x^*)≥0
\end{cases} \\
$$

## 罚函数法
罚函数是一种将约束问题转化为无约束问题的方法。
### 外罚函数法
概念：通过增加罚函数的方法，将约束问题转化为无约束问题，然后用无约束问题的方法求解。因为$x(\sigma) \notin D$, 所以$x(\sigma)$是从可行域外部逼近可行域的，所以称为外罚函数法。  
一般化的优化问题：
$$
\begin{cases}
\min\limits_{x\in R^n}f(x)\\
s.t. h_i(x)=0, i\in E=\{1,2,...,l\}\\
g_j(x)\geq0, i\in I=\{1,2,...,m\}
\end{cases}
$$
可行域 
$D=\{x\in R^n|h_i(x)=0(i\in E), g_j(x)\geq0(i\in I)\}$  
构造罚函数 
$\overline{P}(x)=\sum\limits_{i\in E}^lh_i(x)^2+\sum\limits_{i\in I}^m[\min\{0,g_j(x)\}]^2$  
增广目标函数
$P(x,\sigma)=f(x)+\sigma\overline{P}(x)$
于是，原问题转化为无约束问题：
$$
\min\limits_{x\in D}P(x,\sigma_k)=f(x)+\sigma_k\overline{P}(x), \sigma_k \rightarrow \infty
$$
算法步骤：
1. 选取初始点$x_0\in R^n$，给定终止误差$0\leq\epsilon\ll1$。设$\sigma>0$, $\gamma>0$。置$k=1$；
2. 求解无约束问题$\min\limits_{x\in R^n}P(x,\sigma_k)=f(x)+\sigma_k\overline{P}(x)$,得到近似解$x_k$；
3. 若$\sigma_k\overline{P}(x_k)\leq\epsilon$，停止迭代，得到近似解$x^*=x_k$；否则，转4；
4. 令$\sigma_{k+1}=\gamma\sigma_k$，置$k=k+1$，转2。
#### 解题方法
求解$\min\limits_{x\in R^n}P(x,\sigma_k)=f(x)+\sigma_k\overline{P}(x)$，即求解$\min\limits_{x\in R^n}f(x)+\sigma_k\overline{P}(x)$，即P对每个变量求偏导，令偏导为0，得到方程组X关于$\sigma_k$的解，令$\sigma_k$趋近于无穷大，得到近似解$x_k$；
### 内点法
概念：通过增加罚函数的方法，将约束问题转化为无约束问题，然后用无约束问题的方法求解。因为$x(\sigma) \in D$, 所以$x(\sigma)$是从可行域内部逼近可行域的，所以称为内点法。内点法只适用于约束条件为不等式且内点可行域非空的情况。  
一般化的优化问题：
$$
\begin{cases}
\min\limits_{x\in R^n}f(x)\\
s.t. g_j(x)\geq0, i\in I=\{1,2,...,m\}
\end{cases}
$$
可行域  
$D=\{x\in R^n|g_j(x)\geq0(i\in I)\}\neq\emptyset$  
障碍函数  
$\overline{H}(x)=\sum\limits_{i\in I}^m-\ln g_i(x)$或者$\overline{H}(x)=\sum\limits_{i\in I}^m\frac{1}{g_i(x)}$  
增广目标函数  
$H(x,\tau)=f(x)+\tau\overline{H}(x)$
于是，原问题转化为无约束问题：
$$
\min\limits_{x\in D}H(x,\tau_k)=f(x)+\tau_k\overline{H}(x), \tau_k \rightarrow 0
$$
算法步骤：
1. 选取初始点$x_0\in D_0$，给定终止误差$0\leq\epsilon\ll1$。设$\tau_1>0$, $\rho>0$。置$k=1$；
2. 求解无约束问题$\min\limits_{x\in R^n}H(x,\tau_k)=f(x)+\tau_k\overline{H}(x)$，得到近似解$x_k$；
3. 若$\tau_k\overline{H}(x_k)\leq\epsilon$，停止迭代，得到近似解$x^*=x_k$；否则，转4；
4. 令$\tau_{k+1}=\rho\tau_k$，置$k=k+1$，转2。
#### 解题方法
求解$\min\limits_{x\in R^n}H(x,\tau_k)=f(x)+\tau_k\overline{H}(x)$，即求解$\min\limits_{x\in R^n}f(x)+\tau_k\overline{H}(x)$，即H对每个变量求偏导，令偏导为0，得到方程组X关于$\tau_k$的解，令$\tau_k$趋近于0，得到近似解$x_k$；
### 乘子法(不考)
概念：通过增加乘子的方法，引入拉格朗日函数，将约束问题转化为无约束问题，然后用无约束问题的方法求解。
#### 等式约束问题的乘子法
一般化的优化问题：
$$
\begin{cases}
\min\limits_{x\in R^n}f(x)\\
s.t. h_i(x)=0, i\in E=\{1,2,...,l\}
\end{cases}
$$
可行域  
$D=\{x\in R^n|h_i(x)=0(i\in E)\}$  
拉格朗日函数  
$L(x,\lambda)=f(x)-\lambda^Th(x), \lambda=(\lambda_1,\lambda_2,...,\lambda_l)^T$  
增广目标函数  
$\psi(x,\lambda, \sigma)=L(x,\lambda) +\frac{\sigma}{2}\|h(x)\|^2$  
于是，原问题转化为无约束问题：
$$
\min\limits_{x\in D}\psi(x,\lambda, \sigma)=L(x,\lambda) +\frac{\sigma}{2}\|h(x)\|^2, \sigma > 0
$$
PH算法步骤：
1. 选取初始值。选取初始点$x_0\in R^n$，$\lambda_1\in R^n$ 给定终止误差$0\leq\epsilon\ll1$。设$\sigma_1>0$, $\gamma>0$, $\nu\in(0,1)$, $\eta>1$。置$k=1$；
2. 求解子问题。求解无约束问题$\min\limits_{x\in R^n}\psi(x,\lambda_k, \sigma_k)=L(x,\lambda_k) +\frac{\sigma_k}{2}\|h(x)\|^2$，得到近似解$x_k$；
3. 检验终止条件。若$\|h(x_k)\|\leq\epsilon$，停止迭代，得到近似解$x^*=x_k$；否则，转4；
4. 更新罚函数。若$\|h(x_k)\|\geq\nu\|h(x_{k-1})\|$，令$\sigma_{k+1}=\eta\sigma_k$，否则，$\sigma_{k+1}=\sigma_k$;
5. 更新乘子。令$\lambda_{k+1}=\lambda_k-\sigma_kh(x_k)$，置$k=k+1$，转2。