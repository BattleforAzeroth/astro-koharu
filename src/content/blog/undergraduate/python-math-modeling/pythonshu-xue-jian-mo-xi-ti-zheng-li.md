---
title: Python数学建模习题整理
link: pythonshu-xue-jian-mo-xi-ti-zheng-li
date: 2023-8-20 11:41:57
categories:
  - - 本科作业
    - Python数学建模
tags:
  - Python
  - 数学建模
math: true
---

:::info
以下为个人学习笔记和习题整理
课程：Python 数学建模
教材：Python 数学实验与建模 司守奎 孙玺菁 编著
:::
:::warning
本作业为对应教材中的习题，持续施工中...
:::
# 第二章 数据处理与可视化

## 习题 2.8
在同一个图形界面中分别画出 6 条曲线
$$y=kx^2\sin(x)+2k+\cos\left(x^3\right),k=1,2,\dots,6.$$

+++danger 解答
```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-10 * np.pi, 10 * np.pi, 10000)
k = range(1, 7)
plt.rc('font', size=16)
plt.rc('text', usetex=True)
plt.title('$y=kx^2sin(x)+2k+cos(x^3)$')
for i in k:
    y = i * x ** 2 * np.sin(x) + 2 * i + np.cos(x ** 3)
    plt.plot(x, y, label='k={}'.format(i))
plt.legend()
plt.show()
```
+++

## 习题 2.9
把屏幕开成 2 行 3 列 6 个子窗口，每个子窗口画一条曲线，画出曲线
$$y=kx^2\sin(x)+2k+\cos\left(x^3\right),k=1,2,\dots,6.$$

+++warning 解答
```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-10 * np.pi, 10 * np.pi, 10000)
k = range(1, 7)
for i in k:
    ax = plt.subplot(2, 3, i)
    y = i * x ** 2 * np.sin(x) + 2 * i + np.cos(x ** 3)
    ax.plot(x,y,'r',label='k={}'.format(i))
    plt.legend()
plt.show()
```
+++

## 习题 2.10
分别画出下列二次曲面
1. 单叶双曲面 $\dfrac{x^2}{8}+\dfrac{y^2}{10}-\dfrac{z^2}{6}=1$
2. 双叶双曲面 $\dfrac{x^2}{8}-\dfrac{y^2}{12}-\dfrac{z^2}{8}=1$
3. 椭圆抛物面 $\dfrac{x^2}{10}+\dfrac{y^2}{6}=z$

+++success 解答
```python 单叶双曲面
from sympy.plotting import plot3d
from sympy.abc import x, y
from sympy.functions import sqrt

plot3d(sqrt(6 / 8 * x ** 2 + 6 / 10 * y ** 2 - 6), (x, -10, 10), (y, -10, 10))
```
```python 双叶双曲面
from sympy.plotting import plot3d
from sympy.abc import x, y
from sympy.functions import sqrt

plot3d(sqrt(x ** 2 - 8 / 12 * y ** 2 - 8), (x, -10, 10), (y, -10, 10))
```
```python 椭圆抛物面
from sympy.plotting import plot3d
from sympy.abc import x, y

plot3d(x ** 2 / 10 + y ** 2 / 6, (x, -10, 10), (y, -10, 10))
```
+++

## 习题 2.11
默比乌斯带是一种拓扑学结构，它只有一个面和一个边界，是 1858 年由德国数学家、天文学家默比乌斯和约翰·李斯丁独立发现的．其参数方程为
$$
\begin{dcases}
x=\left(2+\dfrac{s}{2}\cos\dfrac{t}{2}\right)\cos t, \\
y=\left(2+\dfrac{s}{2}\cos\dfrac{t}{2}\right)\sin t, \\
z=\dfrac{s}{2}\sin\dfrac{t}{2}
\end{dcases}
$$
其中，$0\le t\le 2\pi,-1\le s\le1$．绘制默比乌斯带．

+++info 解答
```python
import matplotlib.pyplot as plt
import numpy as np

ax = plt.axes(projection='3d')
t = np.linspace(0, 2 * np.pi, 1000)
s = np.linspace(-1, 1, 1000)
S, T = np.meshgrid(s, t)
X = (2 + S / 2 * np.cos(T / 2)) * np.cos(T)
Y = (2 + S / 2 * np.cos(T / 2)) * np.sin(T)
Z = S / 2 * np.sin(T / 2)
ax.plot_surface(X, Y, Z, cmap='viridis')
plt.show()
```
+++

# 第三章 Python 数学应用
## 习题 3.6
求解下列线性方程组


$$\begin{dcases} x_1+2x_2+x_3-x_4=0 \\ 3x_1+6x_2-x_3-3x_4=0 \\ 5x_1+10x_2+x_3-5x_4=0 \end{dcases}$$
2. 
$$\begin{dcases} 2x+y-z+w=1 \\ 4x+2y-2z+w=2 \\ 2x+y-z-w=1 \end{dcases}$$
+++primary 解答
```python
import sympy as sp


def solve(A, b):
    if b == sp.zeros(b.shape[0], b.shape[1]):  # 齐次方程
        print("基础解系为：", A.nullspace())
    else:  # 非齐次方程
        n = A.shape[1]  # 未知数个数
        C = A.row_join(b)  # 构造增广矩阵
        c = C.rref()[1]  # 主元列
        C = C.rref()[0]
        print("通解为：")
        k = 1
        for i in range(n):
            if i not in c:
                M = C[0:len(c), i]
                M = -M
                t = sp.zeros(n - len(c), 1)
                t[k - 1] += 1

                for j in range(len(c)):
                    t = t.row_insert(c[j], M.row(j))

                print('c' + str(k) + ' *', t, '+ ', end='')
                k += 1
        M = C[0:len(c), -1]
        t = sp.zeros(n - len(c), 1)
        for j in range(len(c)):
            t = t.row_insert(c[j], M.row(j))

        print(t)


if __name__ == '__main__':
    A1 = sp.Matrix([[1, 2, 1, -1], [3, 6, -1, -3], [5, 10, 1, -5]])
    b1 = sp.Matrix([0, 0, 0])
    b1.transpose()
    A2 = sp.Matrix([[2, 1, -1, 1], [4, 2, -2, 1], [2, 1, -1, -1]])
    b2 = sp.Matrix([1, 2, 1])
    solve(A1, b1)
    solve(A2, b2)
```
+++

## 习题 3.7
先判断下列线性方程组解的情况，然后求对应的唯一解、最小二乘解或最小范数解


$$\begin{dcases} 4x_1+2x_2-x_3=2 \\ 3x_1-x_2+2x_3=10 \\ 11x_1+3x_2=8 \end{dcases}$$
2. 
$$\begin{dcases} 2x+3y+z=4 \\ x-2y+4z=-5 \\ 3x+8y-2z=13 \\ 4x-y+9z=-6 \end{dcases}$$

+++danger 解答
```python
import numpy as np
import numpy.linalg as LA


def solve(A, b):
    RA = LA.matrix_rank(A)
    C = np.append(A, b, axis=1)  # 增广阵
    # print(C)
    RAb = LA.matrix_rank(C)
    if RA < RAb:
        print("无解，最小二乘解为：", LA.pinv(A).dot(b))
    elif RA == A.shape[1]:
        print("有唯一解：", LA.solve(A, b))
    else:
        print("有多解，最小范数解为：", LA.pinv(A).dot(b))


if __name__ == '__main__':
    A1 = np.array([[4, 2, -1], [3, -1, 2], [11, 3, 0]])
    b1 = np.array([[2, 10, 8]])
    b1 = b1.reshape(3, 1)
    A2 = np.array([[2, 3, 1], [1, -2, 4], [3, 8, -2], [4, -1, 9]])
    b2 = np.array([[4, -5, 13, -6]])
    b2 = b2.reshape(4, 1)
    solve(A1, b1)
    solve(A2, b2)
```
+++

# 第四章 概率论与数理统计

## 习题 4.1
一家工厂生产的某种元件的寿命 X（以 h 计）服从均值$\mu = 160$，标准差$\sigma (\sigma >0)$的正态分布，若要求$P\{120<X\le200\}\ge0.80$，允许$\sigma$最大为多少？

+++warning 解答
```python
from scipy.stats import norm
from scipy.optimize import fsolve

f = lambda sigma: norm.cdf(200, 160, sigma) - norm.cdf(120, 160, sigma) - 0.8
print("sigma=", fsolve(f, 10))
```
+++

# 附：Windows 系统 Python 数学建模环境安装

## 安装 PyCharm
安装 PyCharm Professional 或者先安装 Toolbox
!!谁能拒绝 JetBrains 啊快跟我一起下 Toolbox!! 

### 安装 Toolbox
Windows 系统从 Toolbox 官网下载 exe 安装包并安装
{% links %}
- site: JetBrains Toolbox 官网
url: https://www.jetbrains.com/zh-cn/toolbox-app/
desc: 点击进入 JetBrains Toolbox 官网下载界面
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/toolbox.png
  color: "#c01fd9"
{% endlinks %}

### 修改 Toolbox 默认安装路径
当前时间下从 Toolbox 的设置中，发现下载路径是只读不可修改
在路径`C:\Users\用户名\AppData\Local\JetBrains\Toolbox`下修改`.settings.json`文件增加安装路径：
```json
"install_location": "E:\\JetBrains",
```
+++danger 注意符合 json 语法，例如：
```json
{
"install_location": "E:\\JetBrains",
"channel_rollback_max_history": 1,
"shell_scripts": {
"location": "C:\\Users\\用户名\\AppData\\Local\\JetBrains\\Toolbox\\scripts"
},
"ui": {
"language": "zh-CN"
},
"tools": {
"localize_tools": true
},
"update": {
"install_automatically": false
}
}
```
+++
设置完成后，直接从 Toolbox 安装 PyCharm Professional

### 激活诀窍
{% links %}
- site: https://jetbra.in/s
  url: https://jetbra.in/s
desc: 点击进入网页下载 jetbra.zip
color: "#ea606e"
{% endlinks %}
打开上述网页后选择一个有效链接并进入，根据上方提示信息点击下载`jetbra.zip`文件
解压后放在你想放的位置，运行`scripts`目录下`install-all-users.vbs`
在之前的网站上找到对应软件，点击下方的`Copy to clipboard`按钮，并看到`Copied!`提示
打开 IDE，粘贴激活码，呈绿色，此时可点击`Activate`激活
安装中文语言包：未打开项目首页`Plugins`，或项目内`File-Settings-Plugins`，搜索`chinese`

## 安装 conda
节省内存，可安装`miniconda`，下载`Python 3.10`版本的最新版
{% links %}
- site: miniconda 下载界面
url: https://docs.conda.io/projects/miniconda/en/latest/miniconda-other-installer-links.html
desc: 下载 Windows installers
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/conda.png
  color: "#41af28"
{% endlinks %}

安装完成后，选择`miniconda3`文件夹属性，在安全标签中给当前用户完全控制权
（此步骤便于将虚拟环境置于`miniconda3`文件夹内部，若跳过此步骤将导致只能通过管理员权限新建虚拟环境）

## 配置环境
若 C 盘空间紧张，可打开`Anaconda Powershell Prompt(miniconda3)`程序，运行`conda info`
查看`package cache`和`envs directories`的默认目录是否在 C 盘
如需修改此目录，可新建或修改用户目录下的`.condarc`文件，例如：

```xml
envs_dirs:
  - E:\miniconda3\envs
pkgs_dirs:
  - E:\miniconda3\pkgs
```

可使用 PyCharm 新建 conda 环境：
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E6%95%B0%E5%AD%A6%E5%BB%BA%E6%A8%A1.1.png#pic_center)

安装 Python 包，可直接在 PyCharm 中打开终端，例如安装 numpy：
```bash
conda install numpy
```