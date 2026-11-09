---
title: 计算方法习题整理（中国MOOC大连理工大学张宏伟）
link: ji-suan-fang-fa-xi-ti-zheng-li-zhong-guo-moocda-lian-li-gong-da-xue-zhang-hong-wei
date: 2023-10-08 20:59:10
categories:
  - - 研究生作业
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%96%B9%E6%B3%95.cover.png
tags:
  - 计算方法
math: true
quiz: true
---

:::info
以下为本年（2023 年秋季）和往年（2021 年春季）网课测验题及作业题整理
课程：计算方法
教材：计算机科学计算（第 2 版） 张宏伟 金光日 施吉林 董波 编著
:::
:::warning
持续缓慢施工中（优先整理本年习题）...
:::
# 第一章 绪论
## 单元测验题
### 选择题
1. 记$\boldsymbol{x}=\left(x_{1},x_{2},x_{3}\right)^{T}\in\mathbb{R}^{3}$，如下定义的函数构成$\mathbb{R}^{3}$上的向量范数的为 []{.gap} 。 {.quiz}
    - $\|x\|=|x_1+x_2|+|x_3|$
    - $\|x\|=|x_1|+2|x_2|+3|x_3|$ {.correct}
    - $\|x\|=|x_1|+2|x_2|-3|x_3|$
    - $\|x\|=|x_1-x_2|+|x_3|$
{.options}

2. 已知$\pi=3.1415926\cdots$，问以下近似值具有最多位有效数字的是 []{.gap} 。 {.quiz}
    - $3.142$
    - $22/7$
    - $3.1415$
    - $3.1416$ {.correct}
{.options}

3. ‍已知近似值$a=138.00$的绝对误差限均为$0.005$，则它有 []{.gap} 位有效数字？ {.quiz}
    - 2
    - 5 {.correct}
    - 4
    - 3
{.options}

4. $a=2.34$是$x= 2.3436\cdots$的近似值，则 []{.gap} 。 {.quiz}
    - a 有 2 位有效数字，且$\left|\dfrac{x-a}a\right|\leq\dfrac{1}{2}\times10^{-2}$ .
    - a 有 3 位有效数字，且$\left|\dfrac{x-a}a\right|\leq\dfrac{1}{2}\times10^{-2}$ .
    - a 有 3 位有效数字，且$\left|\dfrac{x-a}a\right|\leq\dfrac{1}{4}\times10^{-2}$ .  {.correct}
    - a 有 2 位有效数字，且$\left|\dfrac{x-a}a\right|\leq\dfrac{1}{4}\times10^{-2}$ .
{.options}

5. 设 x 为精确值，a 是其近似值，且$\dfrac{\left|x-a\right|}{\left|a\right|}\leq\dfrac{1}{2}\times10^{-4}$，则$\left|\dfrac{\sqrt[3]{x}-\sqrt[3]{a}}{\sqrt[3]{a}}\right|\leq$ []{.gap} 。 {.quiz}
    - $\dfrac16{\times}10^{-4}$ .  {.correct}
    - $\dfrac17{\times}10^{-4}$ .
    - $\dfrac18{\times}10^{-4}$ .
    - $10^{-5}$ .
{.options}

6. 矩阵$\begin{pmatrix}
   1 & -1 & 1 \\
   1 & 0 & -1 \\
   0 & 1 & -1
   \end{pmatrix}$的 F-范数为 []{.gap} 。 {.quiz}
    - $\sqrt7$ {.correct}
    - $1$
    - $7$
    - $3$
{.options}

7. 设$A=\begin{pmatrix}
   1 & 2 & -5 \\
   3 & -6 & 2
   \end{pmatrix}$则 []{.gap} 。 {.quiz}
    - $\begin{Vmatrix}A\end{Vmatrix}_1=11,\begin{Vmatrix}A\end{Vmatrix}_\infty=8$
    - $\begin{Vmatrix}A\end{Vmatrix}_1=2,\begin{Vmatrix}A\end{Vmatrix}_\infty=4$
    - $\begin{Vmatrix}A\end{Vmatrix}_1=4,\begin{Vmatrix}A\end{Vmatrix}_\infty=2$
    - $\begin{Vmatrix}A\end{Vmatrix}_1=8,\begin{Vmatrix}A\end{Vmatrix}_\infty=11$ {.correct}
{.options}

8. 在矩阵空间$\mathbb{C}^{n\times n}$中,对于$A=\left(a_{ij}\right)_{n\times n}$以下哪个函数可以作为矩阵范数？[]{.gap} 。 {.quiz}
    - $\sqrt{\rho(A^{\mathrm{H}}A)}$ .  {.correct}
    - $\rho(A)$ .
    - $\left|\displaystyle\sum_{i=1}^n\displaystyle\sum_{j=1}^na_{ij}\right|$ .
    - $\begin{vmatrix}\det(A)\end{vmatrix}$ .
{.options}

9. 设$a=1.25$和$b=2.75$分别是$x=1.25333\cdots$和$y=2.7456\cdots$的近似值，则$\begin{vmatrix}xy-ab\end{vmatrix}\leq$ []{.gap} 。 {.quiz}
    - $2\times 10^{-3}$ .
    - $2\times 10^{-2}$ .  {.correct}
    - $4\times 10^{-3}$ .
    - $\dfrac12 \times 10^{-3}$ .
{.options}

10. 在如下的这四种矩阵范数中，不是矩阵的算子范数的是 []{.gap} 。 {.quiz}
    - F 范数 {.correct}
    - 2 范数
    - 1 范数
    - 无穷范数
{.options}

11. 已知$e=2.71828\cdots$，则近似值$a=2.7182$的相对误差界为 []{.gap} 。{.quiz}
    - $\dfrac14\times 10^{-2}$ .
    - $\dfrac14\times 10^{-1}$ .
    - $\dfrac14\times 10^{-3}$ . {.correct}
    - $\dfrac14\times 10^{-4}$ .
{.options}

### 判断题
1. 最早提出多项式求值运算次数最少的算法的是中国南宋数学家秦九韶。 {.quiz .true}

2. 绝对误差一定是正的。 {.quiz .false}

3. 谱半径可以作为矩阵范数。 {.quiz .false}

### 填空题
1. 已知$a=1.234,b=2.345$分别是 x 和 y 的具有 4 位有效数字的近似值，那么$\left|(3x-y)-(3a-b)\right|\leq$  [2]{.gap} ×10¯³ {.quiz .fill}

2. 设$a=211.00112$为 x 的近似值，且$|x-a|\leq0.5\times10^{-2}$，则 a 至少有 [5]{.gap} 位有效数字。 {.quiz .fill}

3. $x=\left(3,0,-4,1\right)^T\in\mathbf{R}^4$，则$\left\|x\right\|_1=$ [8]{.gap} 。 {.quiz .fill}

4. $x=\left(3,0,-4,1\right)^T\in\mathbf{R}^4$，则$\|x\|_\infty=$ [4]{.gap} 。 {.quiz .fill}

5. $x=\left(3,0,-4,1\right)^T\in\mathbf{R}^4$，则$\left\|x\right\|_2^2=$ [26]{.gap} 。 {.quiz .fill}

6. $x=\left(3,0,-4,1\right)^T\in\mathbf{R}^4$，则$\left\|x\right\|_3^3=$ [92]{.gap} 。 {.quiz .fill}

7. 已知 a 的相对误差界为 0.002,则$a^m$的相对误差界为 [2]{.gap} m×10¯³ {.quiz .fill}


