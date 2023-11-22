# Opimization

## Hessian矩阵 与 严格全局极小点
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

## 序列收敛
### 概念
对于$\lim\limits_{k\to\infty}\frac{\|x_{k+1}-x^*\|}{\|x_k-x^*\|^p}=q$
1. 线性收敛：$0<q<1, p=1$
2. 超线性收敛：$q=0, p=1$
3. p阶收敛：$q=C, p>1$
$x^*$是序列的极限点。

## 牛顿迭代法
### 概念
牛顿迭代法是一种求解方程的迭代方法，它是一种二阶收敛的方法。  
它的思想是: 用一阶泰勒展开式去逼近函数，然后求解逼近的方程，得到下一个迭代点，直到满足终止条件。  
一阶函数牛顿法公式 ： $x_{k+1}=x_k-\frac{f(x_k)}{f'(x_k)}$  
多元函数牛顿法公式 ： $x_{k+1}=x_k-H_k^{-1}g_k$ , $H_k$是$f(x_k)$的Hessian矩阵，$g_k$是$f(x_k)$的梯度。  
阻尼牛顿法公式： $x_{k+1}=x_k-\lambda_kH_k^{-1}g_k$ , $\lambda_k$是步长，增加线性搜索，防止迭代点跑出函数定义域。
### 阻尼牛顿法步骤
1. 选取初始点$x_0$，给定终止误差$\epsilon$，置$k=0$；
2. 计算$f(x_k)$的梯度$g_k$，当$\|g_k\|<\epsilon$时，停止迭代，得到近似解$x^*=x_k$；否则，进行第3步；
3. 计算$f(x_k)$的Hessian矩阵$H_k$，计算阻尼因子$\lambda_k$，计算下一个迭代点$x_{k+1}=x_k-\lambda_kH_k^{-1}g_k$，置$k=k+1$，转第2步。
4. 阻尼因子$\lambda_k$的计算方法有很多种，这里介绍一种：$\lambda_k=\min\{1,\frac{1}{2}\|\nabla f(x_k)\|_2\}$
5. 令$x_{k+1}=x_k-\lambda_kH_k^{-1}g_k$，置$k=k+1$，转第2步。

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

## 最速梯度下降法
### 概念
最速梯度下降法是梯度下降法的一种改进方法。  
它的思想是：负方向梯度的方向是函数下降最快的方向，所以在每一步迭代中，沿着负梯度方向进行迭代，可以使得函数值下降最快。因此，取当前迭代点的负梯度方向作为搜索方向，进行一维搜索，找到最优步长，然后沿着该方向进行迭代，直到满足终止条件。
### 步骤
#### 最速梯度下降法计算步骤
1. 选取初始点$x_0$，给定终止误差$\epsilon$，置$k=0$；
2. 计算$f(x_k)$的梯度$g_k$，当$\|g_k\|<\epsilon$时，停止迭代，得到近似解$x^*=x_k$；否则，进行第3步；
3. 取$p_k=-g_k$；
4. 进行一维搜索，即求$\lambda_k$，使得$f(x_k+\lambda_kp_k)=\min\limits_{\lambda\geq0}f(x_k+\lambda p_k)$；
5. 令$x_{k+1}=x_k+\lambda_kp_k$，置$k=k+1$，转第2步。
#### 最优步长计算步骤
微分法
因为要找寻$\lambda$使得$f(x_k+\lambda p_k)=\min\limits_{\lambda\geq0}f(x_k+\lambda p_k)$，所以可以对$f(x_k+\lambda p_k)$求导，令导数为0，求得最优步长$\lambda$。

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
    lamda = 0
    while True:
        g = grad(x1, x2)
        print(f'{i}Turn,x1={x1}, x2={x2}, f(x1, x2)={f(x1, x2)}, \n\tnorm = {norm(g[0], g[1])}, lamda = {lamda}, g = {g}')
        if norm(g[0], g[1]) < e:
            break
        else:
            p = -g
            lamda = get_lamda(x1, x2, p)
            x1 = x1 - lamda * grad(x1, x2)[0]
            x2 = x2 - lamda * grad(x1, x2)[1]
            x1 = round(x1, 3)
            x2 = round(x2, 3)

steepest_descend_method(10, 10, 0.1)